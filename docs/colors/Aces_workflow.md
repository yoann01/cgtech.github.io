

# ACES Color Pipeline 


``` mermaid 
flowchart LR
  A(Scene Tristimuli) --> B[OECF]
  B --> C[IDT] 
  C --> D[LMT]
  D --> E[RRT]
  E --> F[ODT]
  F --> G[EOCF]
  G --> H(Display Tristimuli)
  C -->|ACES| E
 style A stroke-width:2px,stroke-dasharray: 5 5
 style H stroke-width:2px,stroke-dasharray: 5 5

```

- [x] **Tristimulis** refers to linear light, code value (from 0 to ) are linearly related to the power in the light 
that is entering in the camera lens. those numbers are 12bits and typically we don't have the downstream infrastruture 
that will handle 12 bits well established.

- [x] **OECF** Tippically the first step in the color pipeline is an OECF (**opto electronic conversion function**), in the old days
we will would've call this GAMMA.Built in the camera, 

- [x] **IDT** (input device transform) ingesting data map from one linear light color space to another. 3*3 matrix transform 

!!! note

    IDT:
    >- The Input Device Transform is the transform used to convert the pixel colors of images/videos from specific devices into an ACES      colorspace.

    RRT:
    >- The Reference Rendering Transform prepares scene referred linear data into high dynamic range display referred data. This data is     then meant to be handed over to an ODT to convert the data to be viewed in a specific display type.

    ODT:
    >- The Output Display Transform is responsible for converting the data created by the RRT to data that can be viewed on specific     devices or color-spaces: sRGB, P3, Rec. 709.

 
LMT
RRT
ODT
ROCF
Display Tristimuli

