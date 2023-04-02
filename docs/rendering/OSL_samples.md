## Simple Skin shader

```C
shader my_shader(
    vector I,
    vector N,
    vector T,
    float sigma_a,
    float sigma_s,
    float g,
    float roughness,
    color albedo = color(1, 1, 1),
    float ior = 1.4,
    float multiscattering = 0.5,
    float melanin = 1.0,
    float subsurface_scale = 1.0,
    float specular_scale = 1.0,
    float diffuse_scale = 1.0,
    float melanin_scale = 1.0,
    float scattering_model = 0,
    color sigma_prime_s_coeff = color(0.74, 0.88, 1.01),
    color sigma_prime_a_coeff = color(0.0014, 0.0025, 0.0142),
    output color result = color(0, 0, 0)
)
{
    // Calculate the halfway vector
    vector H = normalize(I + N);

    // Calculate the diffuse term
    color diffuse = albedo / M_PI;

    // Calculate the specular term
    color specular = pow(max(dot(H, N), 0.0), 5);

    // Calculate the Beckmann term
    color beckmann = exp(-pow(dot(N, H), 2) / (pow(tan(acos(dot(N, H))), 2) * pow(roughness, 2))) / (M_PI * pow(roughness, 2) * pow(dot(N, H), 4));

    // Calculate the absorption term
    color absorption = exp(-2 * (sigma_a + sigma_s) * dot(N, H));

    // Calculate the reduced scattering term
    color reduced_scattering = (1 - g) / (1 + (1 - g) * pow(dot(N, H), 2));

    // Calculate the phase function term
    color phase_function = 0.25 / M_PI * (1 + pow(dot(N, H), 2));

    // Calculate the Fresnel term
    color fresnel = (1 - pow(ior, 2)) / (1 + pow(ior, 2) - 2 * ior * dot(I, H));

    // Calculate the melanin term
    color melanin_term = melanin * (sigma_a + sigma_s);

    // Calculate the spectral model for skin scattering
    color spectral_model = 0;
    if (scattering_model == 0)
    {
        // Calculate the spectral model using the skin_scattering function
        spectral_model = skin_scattering(N, H, sigma_prime_s_coeff, sigma_prime_a_coeff);
    }
    else if (scattering_model == 1)
    {
        // Calculate the spectral model using the Henyey-Greenstein model
        spectral_model = henyey_greenstein(N, H, g);
    }
    else if (scattering_model == 2)
    {
        // Calculate the spectral model using the Schlick model
        spectral_model = schlick(N, H, g);
    }

    // Calculate the multiple scattering term
    color multiple_scattering = exp(-multiscattering * (sigma_a + sigma_s));

    // Calculate the final color
    result = (diffuse + specular * beckmann * absorption * reduced_scattering * phase_function * fresnel * spectral_model * multiple_scattering) / sigma_t;

    // Scale the diffuse, specular, subsurface, and melanin contributions
    result *= diffuse_scale;
    result *= specular_scale;
    result += melanin_term * melanin_scale;
    result += melanin_term * subsurface_scale;

    // Calculate the tangent space basis vectors
    vector U = normalize(T - dot(T, N) * N);
    vector V = normalize(cross(N, U));

    // Calculate the tangent space direction of the incident light
    vector I_tangent = vector(dot(I, U), dot(I, V), dot(I, N));

    // Calculate the BRDF in tangent space
    color brdf_tangent = (diffuse + specular * beckmann * absorption * reduced_scattering * phase_function * fresnel * spectral_model * multiple_scattering) / sigma_t;

    // Transform the BRDF back to world space
    result = color(
        dot(brdf_tangent, vector(U.x, V.x, N.x)),
        dot(brdf_tangent, vector(U.y, V.y, N.y)),
        dot(brdf_tangent, vector(U.z, V.z, N.z))
    );
}

// Function to calculate the spectral model for skin scattering
color skin_scattering(vector N, vector H, color sigma_prime_s_coeff, color sigma_prime_a_coeff)
{
    // Calculate the skin scattering coefficients
    color sigma_prime_s = sigma_prime_s_coeff * (1 + 0.01 * pow(dot(N, H), 2));
    color sigma_prime_a = sigma_prime_a_coeff * (1 + 0.0001 * pow(dot(N, H), 2));

    // Calculate the reduced scattering term
    color reduced_scattering = (1 - g) / (1 + (1 - g) * pow(dot(N, H), 2));

    // Calculate the spectral model for skin scattering
    return sigma_prime_s / (sigma_prime_s + sigma_prime_a);
}

// Function to calculate the spectral model using the Henyey-Greenstein model
color henyey_greenstein(vector N, vector H, float g)
{
    return 1 / (4 * M_PI) * (1 - pow(g, 2)) / pow(1 + pow(g, 2) - 2 * g * dot(N, H), 1.5);
}

// Function to calculate the spectral model using the Schlick model
color schlick(vector N, vector H, float g)
{
    return 1 / (4 * M_PI) * (1 + pow(g, 2)) / pow(1 + pow(g, 2) - 2 * g * dot(N, H), 1.5);
}

```

In this updated implementation, the scattering_model parameter allows the user to choose between three different models for calculating the spectral model: the default skin scattering model, the Henyey-Greenstein model, or the Schlick model.

The sigma_prime_s_coeff and sigma_prime_a_coeff parameters allow the user to adjust the coefficients for the sigma prime s and sigma prime a values in the skin scattering model. 

Additionally, the multiscattering parameter allows the user to adjust the amount of multiple scattering applied to the skin, and the subsurface_scale, specular_scale, diffuse_scale, and melanin_scale parameters allow the user to adjust the relative contributions of the subsurface, specular, diffuse, and melanin terms in the final color calculation.


A Spectral BSSRDF for Shading Human Skin" and "Practical and Controllable Subsurface Scattering for Production Path Tracing" 


## Probability shader

```C

shader my_shader(
    output color result = color(0, 0, 0)
)
{
    // Use the rand() function to generate a random value between 0 and 1
    float random = rand();

    // Use the random value to determine the output color
    if (random < 0.33) {
        // Output red
        result = color(1, 0, 0);
    } else if (random < 0.66) {
        // Output green
        result = color(0, 1, 0);
    } else {
        // Output blue
        result = color(0, 0, 1);
    }
}

```