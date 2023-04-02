# NOTES


## ACEScg Conversion Cheat Sheet
!!! note
    Textures for 3D materials:

      - [x] You need to preserve the look of the colors?: **Utility - sRGB - Texture**

        >- Diffuse
        >- SSS
        >- Albedo
        >- Spec
        >- Metallicity

      - [x] You need to preserve the numeric values of you pixels?: **Utility - Raw**

        >- Bump
        >- Normal
        >- Displacement

      - [x] You need your image to look as though you opened it up in Photoshop?: **Output - sRGB**

        >- Backplates or Compositing

## Abbreviations
!!! note


    >- ACES - Academy Color Encoding System

    >- AMPAS - Academy of Motion Picture Arts and Science

    >- OCIO - Open Color IO

    >- OIIO - Open Image IO

    >- LUT - Look Up Table

    >- ICC - International Color Consortium

    >- ICM - Image Color Management
  
    >- IDT - Input Device Transform

    >- ODT - Output Device Transform

    >- LMT - Look Modification Transform

    >- RRT - Reference Rendering Transform

    >- UI - Unsigned Integer

    >- OCES - Output Color Encoding Specification


## CIExy 1931 Color Diagram
This is a very common diagram depicting the extent of colors humans can perceive. It is important to note that the diagram does not depict value/intensity only hue and saturation. To explain gamut, primaries, and white points I will be using a CIExy diagram to visualize color-spaces so we can easily see the size of a colorspace and how much of the visual light spectrum can be represented by these colorspaces.

## gamut
A colorspace's gamut is the set of all the colors that can be represented within that colorspace. In the diagram below the gamut is the set of all the colors within the colorspace triangle. Many popular gamuts have been graphed to help illustrate the wide range to pick from. Notice how few colors can actually be represented by sRGB.


## primaries
For RGB images primaries are your reddest reds, greenest greens, and bluest blues of a color gamut. In the diagrams below you can see these are represented by the corners of the gamut triangles. Also note the position of the green primary of the ACEScg colorspace. It falls outside of the visible spectrum of hues (called an imaginary color). It was placed there so as many hues between rend and green could fall within the ACEScg gamut. One consequence of the primary being where it is is you will never use a fully green value by itself.


## white point 
The white point is the point within a colorspace we consider to be white. ACEScg and sRGB have different white points. Below the Kelvin temperature scale (and P3) is graphed over all human visible hues (CIE 1931 Chromaticity Diagram). Often you will see a white point of a colorspace refered to by its CIE Standard Luminant designation. These usually start with the letter "D" and two numbers. For example ACEScg and sRGB have D60 and D65 white points. These closely translate to a value on the Kelvin scale: D65 is 6500 Kelvin and D60 is 6000 Kelvin.


## gamma 
When dealing with gamma you are going to come across the terms linear and gamma curves quite often. ACES is linear but marjority of the time the images we take with our camera, make in photoshop, and download off the internet are not. So, we need to understand what gamma is and how to make a non-linear image linear. Back when computers were slow, drive space was expensive, and memory was small we needed to store our images in as efficient a manner as possible. First of all we could only store our images using 8 bits per color channel which meant each channel only had 256 individual values it could store. It turns out our eyes are more sensitive to small increases of value in darker colors than in lighter colors. We could store our images using a gamma curve to dedicate more of the 256 values in each channell to the darker colors rather than the lighter ones. This meant as a pixel value increased that value would increase by greater and greater amounts. So, to put it another way, going from 0 to 1 would result in a smaller increase in value than an increase from 254 to 255. In a linear image the value increases are uniform. 3D applications prefer a linear image as it makes the math for calculating color and light a lot easier and it makes using high dynamic range images possible. Understanding if your non-ACES images is linear or has a gamma curve is really important to converting it properly.



Notice for the non-linear curves the values flip after 1. For an images with a dark gamma values begin to brighten after 1 and the oposite for a bright gamma. This is why we need to work with linear images when dealing with values above 1 (HDR iamges).




When doing research on ACES on your own you will often come across the terms scene-referred and display-referred and it is important to understand what they mean and how they relate to your images.

## scene-referred
Scene referred images are linear and are meant to represent real-world light values or light as it actually is. However, they look terrible when displayed raw on a monitor because they don't take into account the characteristics of the display (dynamic range, gamma, etc.). ACES and ACEScg are both Scene-Referred. Scene-referred images have a linear gamma curve.

## display-referred
Display referred images are encoded in a way to make them look good when displayed or has the data encoded in a way affords efficient storage. sRGB, P3, Rec. 709, and Adobe RGB (1998) are all Display-Referred images. Display-Referred images are encoded to be looked at on a specific device (sRGB monitor, Rec. 709 TV, P3 movie screen) or come from a specific camera colorspace (RED DRAGONcolor, ARRI LogC, Sony S-Log, etc.). Display-referred images have a non-linear gamma curve.

