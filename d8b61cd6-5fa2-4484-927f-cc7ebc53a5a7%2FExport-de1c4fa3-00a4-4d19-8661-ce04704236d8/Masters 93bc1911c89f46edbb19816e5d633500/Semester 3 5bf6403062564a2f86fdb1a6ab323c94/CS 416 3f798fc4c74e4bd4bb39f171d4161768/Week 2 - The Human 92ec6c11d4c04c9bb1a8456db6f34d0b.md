# Week 2 - The Human

## The Model Human Processor

- The human
    - Human processes are like a computer processor
        
        ![Untitled](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Untitled.png)
        
    - Humans have working vs long-term memory, motor processor, visual and auditory image stores
        
        ![Untitled](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Untitled%201.png)
        
    - Human eyes jerk around but we don't perceive it
        
        ![Untitled](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Untitled%202.png)
        
    - Fitts law - larger movements are faster but less accurate than smaller ones (T = 600ms + 240ms lg (1 + distance to target / size of target)
- The memory
    - Sensory memory
        - Iconic memory - visual (persistence of vision and half second)
        - Echoic memory - aural
        - Haptic memory - touch
        - Arousal - level of interest or need (amount of attention)
    - Human 'DRAM'
        - 200ms refresh time
        - Recency affect where last is best
    - Human long term memory
        - Two types
            - Episodic - events, organized temporally
            - Semantic - facts, organized associatively
        - Representations
            - Semantic nets (graphs)
            - Frames (database w/field)
            - Scripts (roles, scenes, props)
        - How we remember
            - Time, distribution of practice, concrete is easier than abstract, structure/familiarity help)
        - Decay
            - Logarithmically - forget most early
            - Hosts law - if two really strong memories then the older is more durable
            - Interference - proactive inhibition, retroactive interference (mind blown), emotion (good old days and forget mundane)
- Reasoning
    - Deductive reasoning - logic (eliminated the impossible, whatever remains must be the truth)
    - Inductive - if true for x then true for x+1, true for x then true for all
        - Allows for entering missing data
        - Extrapolation
        - Interpolation - varying smoothly in between individual points (turning scatterplot into line graph)
    - Adductive reasoning - human need for meaning and asking why
        
        ![Untitled](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Untitled%203.png)
        
- Human retina
    - We have a blind spot on the optic nerve
    - Acuity - angular resolution of the retina
        - Snellen ratio - 20/x (you can distinguish at 20 feet what average person can distinguish at X feet)
    - Rods - brightness
        - 80 million
    - Cones - color (red, green, blue cones)
        - 5 million total
        - Luminance = 31 % red, 59% green, 10% blue
    - Ganglions - nerve cells (X-cells detect pattern) (Y-cells detect movement)
        
        ![Untitled](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Untitled%204.png)
        
- Perceiving two dimensions
    - Lateral inhibition
        - Horizontal cells accentuate differences and detect motion
        - This is what leads to many visual eye tricks
        
        ![Screenshot 2023-05-31 at 8.51.39 PM.png](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Screenshot_2023-05-31_at_8.51.39_PM.png)
        
- Perceiving perspective
    - Foreshorting - objects at different depth along similar line of sight project to nearby locations
    - Linear perspective -  objects farther away appear smaller
    - Size constancy - objects do no change size so smaller objects must be farther away than larger objects
    - Perception of size of an object influences or perception of the distance
        - Avoid incorporation of artificial 3d elements in 2d to avoid confusion

## Computer Graphics

- 2D graphics
    
    
    | Vector graphic | Raster graphic |
    | --- | --- |
    | Plotters, laser displays | TVs, phones |
    | Clip art | Photographs |
    | PDF, SVG | GIF, JPG |
    | Low memory | High memory |
    | Easy to draw a line | Hard to draw a line |
    | Solid/gradient/texture fills | Arbitrary fills |
    
    ![Screenshot 2023-06-02 at 3.13.40 PM.png](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Screenshot_2023-06-02_at_3.13.40_PM.png)
    
    - Canvas coordinates - used to define position of vertices for graphic primitives
        - Create canvas for entire visualization
        - Create a sub-canvas for plotting data
        - Canvas —> screen transformation
            - Draw primitives in canvas coordination and use rasterization fills in transformed outline
- 2D drawing
    - SVG (scalable vector graphics) - format specifications for describing 2d graphics
        - Width/height describe size on page
        - viewbox=”x y w h”
            - Start at x and y and extends to x+w and y+h
        - Origin is always upper-left corner
            
            ![Screenshot 2023-06-05 at 9.37.29 PM.png](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Screenshot_2023-06-05_at_9.37.29_PM.png)
            
- 3D graphics
    - We use RGB on computers because it simulates what our eyes can actually see (red/green/blue cones)
        
        ![Screenshot 2023-06-14 at 8.01.14 PM.png](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Screenshot_2023-06-14_at_8.01.14_PM.png)
        
    - Polygonal models
        - Simulate shapes using primitives (for example triangles)
        - Then projected onto 2d display and rasterized into pixels
            
            ![Screenshot 2023-06-14 at 8.03.49 PM.png](Week%202%20-%20The%20Human%2092ec6c11d4c04c9bb1a8456db6f34d0b/Screenshot_2023-06-14_at_8.03.49_PM.png)
            
        - Perspective distortion
            - Things father away are made smaller so that the perspective looks right
- Photorealism
    - Visual perception relies on depth cues that indicate an otherwise flat image represents a 3d scene
        - Cues to perspective system: occlusion, shadowing, perspective, stereopsis, focus, lighting, texturing, attenuation
        - Occlusion
            - Most objects are opaque and hide objects behind them and implies a near to far visual sort
            - Strongest cue
            - Easier to compute for opaque objects than for translucent objects
        - Illumination
            - Cues human visual system to the orientation of a surface
            - Diffuse illumination - surface brightest when facing the light source (implies rough)
            - Specular illumination - brightest when reflecting light source (implies smooth)
        - Shadowing
            - Indicates light occlusion and cues perceptual system to objects relative position to each other
        - Perspective
            - Size constancy cues (objects are the same size but farther ones appear smaller)
        - Stereopsis
            - Rendering from two different viewpoints (one for each eye)
            - View directions should be parallel (not rotated)
            - Useful when other cues are unavailable
- Non-photorealism
    - Departs from limits of photorealism to better communicate, uses concepts from art rather than physics
    - Based on contours instead of surfaces
    - Makes it easier to communicate shape without complex lighting
    - Silhouette curves - constructed from edges shared by front and back facing mesh polygons

## Quiz

- How many items can human working memory (short-term memory) typically hold?
    - **3–7 items**
        - Our working memory can only hold 3–7 items at a time, though a single item in our working memory can be a collection of items in our long-term memory.
- Given a plot of life expectancy based on country and birth year, you look up your country and birth year, find the displayed life expectancy, and conclude you will probably live that long. This is an example of _________________.
    - **Deductive reasoning**
        - This is an example of deductive reasoning because we are drawing the conclusion implied by the given data.
- A light gray box drawn on top of a dark gray background will make the light gray box appear ______________.
    - **Brighter**
        - The dark gray box will make the light gray box appear even brighter because the human visual system's lateral inhibition will detect and accentuate the difference.
- You’re given two circles of the same size. The left one is surrounded by smaller circles and the right one is surrounded by larger circles. Which circle appears larger?
    - **The left one.**
        - The perceptual processing of the human visual system is designed not to ignore differences but to accentuate them.
- When visualizing data, you should keep your eyes focused on one point for the entire duration of the visualization.
    - **False, because your visual system will play tricks on your perception of the data.**
        - As we showed in the slides, focusing on a single point causes a temporal inhibition in the light sensors and can play tricks on your perception.
- On which of these colors does the human eye have the most difficulty focusing?
    - Blue
        - Because of the chromatic aberration of the eye's lens, the blue end of the optical spectrum of light tends to focus off the retina. If you have sharp details that need to be displayed in a shade of blue, try to avoid pure blue hues.
- Which one of the 3-D depth cues below is the strongest?
    - **Occlusion**
        - Occlusion is the strongest cue, because if a point on object A and object B project to the same point on the image plane, the fact that you see object A and not object B at that point provides incontrovertible evidence of a depth ordering that A is closer than B.
- Which one of the 3-D depth cues below indicates surface orientation?
    - **Illumination**
        - Occlusion and shadowing only indicate the surface closest to the observer (or light source), and stereopsis provides relative cues of distance across an image, whereas the illumination of a surface changes based on how the surface is facing the light source (and for specular reflection, the viewer).
- In what order does a data visualization graphics pipeline process information?
    - **Vertex processing, then rasterization, then pixel processing**
        - The graphics pipeline accepts vector graphics primitives described as vertices, so it processes vertices first. Rasterization converts vector graphics primitives into the pixel locations used to display them on a display screen. Pixel processing is used to further process the pixels output from rasterization, e.g., to compute their individual colors.
- Which one of the following is NOT an element of vector graphics?
    - Pixels
        - While vector graphics are sometimes converted to a rectilinear raster graphics array of pixel color values for display on a raster device, some applications work directly from the vector graphics specification, such as a plotter or a laser display.