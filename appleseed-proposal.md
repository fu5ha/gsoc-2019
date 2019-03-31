# [Light Paths Visualization](https://github.com/appleseedhq/appleseed/wiki/List-of-Project-Ideas-for-GSoC-2019#project-10-improve-light-paths-visualization) and Viewport Unification Proposal

## Contact Information

Gray Olson

- Email: [gray@grayolson.com](gray@grayolson.com)
- Discord: Fusha#8156
- GitHub: [termhn](https://github.com/termhn)
- Website: [grayolson.me](https://www.grayolson.me/)

## Abstract

Light path recording is a unique and potentially extremely valuable tool in appleseed; however, it is currently relatively limited in capability of both data capture and visualization. This project aims to help remedy both of these by improving the number of quantities that are able to be recorded, improve the visualization capabilities for these quantities, and provide a method for basic data analysis, filtering, and report generation.

In order to do this, a main piece of the project will be to provide a unified viewport in appleseed.studio which is capable of displaying and switching between several possible views of a scene and overlay data and widgets on top of it. This will greatly improve the usability of appleseed.studio as a scene mastering tool by allowing a technical artist to view exactly how different parts of a render are being affected by lights, objects, etc. and will pave the way for even more useful data integration to be added in the future.

## Main Project Goals

1. Verify and improve light path recording
    * Verify current light path recording is physically accurate
    * Determine and implement other valuable quantities to record with the community and industry
    * Provide configuration for which quantities to record in a given render
2. Provide a unified viewport in appleseed.studio
    * Provide an easy way to switch between the final render and a basic OpenGL-rendered version of the scene
    * Allow multiple passes to be composited together onto the main viewport and provide an interface to toggle them on and off.
3. Improve light paths visualization
    * Create a light path visualization pass which is able to be drawn on top of the final render or the OpenGL version of the scene
    * Implement proper tone mapping, transparency, variable line width, and possibly other indicators based on the recorded light path data
    * Implement more useful filtering of light paths based on recorded data

### Stretch Goals

1. Implement two additional base display modes for the scene:
    * Reprojection of the final render onto OpenGL scene geometry
    * A simple but functional realtime PBR pipeline

## Project Details

### Light Path Recording Details

As described in the original project idea description, the first step will be verifying that the current implementation is correct and annotating it with physical properties. Concurrently, I'll be interacting with appleseed and potentially other community members to determine which other quantities would be useful to have the option of recording. These should also be configurable in the renderer, as sometimes we might not want to record all of them.

### Viewport Details

One of the main pieces of my project will be reworking the viewport in appleseed.studio to unify it. One viewport will provide the ability to view final (or progressive) renders, simplified, realtime OpenGL representation of the scene. In addition, it will be possible to overlay various things on top of the main scene representation, and to integrate these overlays into the main representation's geometry using the scene's z-depth. For my project, I'll be focusing on integrating a visualization of the light paths as well as of the lights and cameras in the scene, however it should also open the door for other overlays like transformation widgets and more.

If time allows, a couple of additional features will be added to the viewport in the form of extra display modes. First, a view mode which re-projects the final render onto scene geometry rendered in realtime using OpenGL to allow moving around the final rendered scene. Second, a basic realtime physically-based pipeline which would provide a way to navigate around a scene in realtime while still retaining a basic idea of what a final render would look like from that perspective.

### Light Path Visualization Details

The improved light paths visualization tool will support displaying all of the recorded quantities, or at least all which could have a succinct visual display cue. It will, as described in the previous section, be able to be integrated into any of the "main" viewport display modes. Paths will be manually triangulated instead of using `GL_LINES` to allow much greater control over thickness and style, and as a bonus, this is actually more performant than using `GL_LINES` depending on the hardware and driver. My initial plan, to be discussed and refined, is:

* The thickness of a light path segment will be proportional (perhaps non-linearly) to the light path's luminance, if the selected piece of data to view is radiance, or a scalar-mapped version of other data quantities, like illuminance if irradiance is selected
* The color of of a light path segment will display either a direct or mapped representation of the currently selected piece of data
* The transparency of an entire light path (all segments) will be configurable globally and will and fade in and out based on filtering of paths
    * Transparency could be a bit tricky to implement as there is not an obvious way to z-order paths or even path segments. Therefore there are basically two options: use an order-independent transparency technique like Weighted Blended Order-Independent Transarency[\[1\]][oit], or use a commutative blend function like addition. The method to be used here should be researched more to determine the best solution, as a commutitive blend function would be much simpler and more performant, but may not give the desired result.

Which brings us to filtering. Light paths should be able to be filtered in the display based by defining a function that maps the recorded data for that light path to a value in `[0, 1]` which will determine its transparency. There should be easy to use, configurable default filter functions on each quantity provided (for example, filtering based on maximum or minimum luminance on a light path), and the ability for a user to define their own filtering function using the raw data, perhaps by defining a python function.

## Project Schedule

I will be on summer break from May 1st to August 22nd, and will be fine to keep working through the final August 26th deadline. I will be out of town from May 1st to May 12th, but will have my computer with me and will still have a significant amount of time to work on things during that time. In addition, there is a possibility of me doing part time work for a couple of weeks in June, however I don't expect this to interfere with my GSoC participation. In addition, I might go out of town for a week or two in July, but I will have my computer with me and still be able to work full time on GSoC while I am out of town.

### Community Bonding

#### Until May 6

- Push my current PRs through to get merged and continue to contribute

#### Until May 13

- Get more familiar with Qt
- Get familiar with appleseed's render pipeline

#### Until May 27

- Begin to collect feedback on which additional quantities would be helpful to collect 

## Phase 1

#### Week of May 27

- Verify correctness of existing radiance recording
- Annotate physical quantities for radiance recording
- Fix errors if there are any

#### Week of June 3

- Begin work on unified viewport by getting the current final render view to be displayed with OpenGL
- Implement the ability to select between the current final render view and the current OpenGL scene view that is used in the light paths tab

#### Week of June 10

- Implement light paths overlay on OpenGL and final render view
- Draw light paths using triangles instead of `GL_LINES`
- Research and finalize transparency solution

#### Week of June 17

- Implement transparency solution
- Bug fixes

## Phase 2

#### Week of June 24

- Finalize new light path recording quantities
- Improve OpenGL view lighting model for better visibility
- Implement a cameras and lights overlay

#### Week of July 1

- Implement new recording quantities
- Determine underlying light path filtering method

#### Week of July 8

- Begin implementing light path filtering

#### Week of July 15

- Finish implementing light path filtering
- Make light path transparency be controlled by the filter output
- Bug fixes

## Phase 3

#### Week of July 22

- Refactor UI/UX if necessary
- Implement default/configurable filtering methods for the different types of recorded data

#### Week of July 29

- Bug fixes, refactoring, and implementation spillover time

#### Week of August 5

- Implement render reprojection onto OpenGL scene

#### Week of August 12

- Begin implementing realtime PBR pipeline
- Begin final report

#### Week of August 19

- Finish implementing basic realtime PBR pipeline
- Final project wrap-up, bug fixes, etc
- Final report modifications
- Final evaluation

## Bio

I introduced myself in Discord previously, but I thought I could go into a little more depth here.

Hi! I'm Gray Olson.

I'm an artist, programmer, gamer, bit-twiddler, and generally curious person from Phoenix, Arizona in the South-West US. I'm studying Drawing at ASU and working towards my BFA, however I am also taking a significant amount of math and computer science, and doing as much programming in my free time as I can. Graphics programming is an amazing intersection many of my favorite subjects (art, programming, math, and gaming). Though I am getting a degree in a non-technical field, right now I think that working as a graphics programmer will be my preferred career path, and I think that having a traditional art background gives me a somewhat unique and valuable viewpoint for this.

I've been contributing to open source projects since I was quite young; I posted my first project to GitHub back when I was in fourth or fifth grade, which was a wrapper around the Bullet physics library for use with Cocos3d. Since then, my contribution has waxed and waned, but in the past year I've enjoyed making fairly consistent contributions to several open source projects as well as starting a few of my own.

My primary projects recently have been related to real-time rendering in the Rust ecosystem, and include contributions to

* https://github.com/gfx-rs/gfx
* https://github.com/omni-viral/rendy
* https://gitlab.com/Veloren/game
* https://github.com/termhn/rendy-pbr

and I am a member of the Amethyst Organization working on the rendering team for the [Amethyst game engine](https://github.com/amethyst/amethyst)

I also have some experience with offline rendering and have written my own small toy path tracer in Rust based on Peter Shirley's Ray Tracing in one Weekend (https://github.com/termhn/rayn). I have also read most of `pbrt` and at one point intended to rewrite `rayn` based on `pbrt`, though that project eventually fell through as I continued working on realtime graphics related projects.

I am not as experienced in C/C++ as I am with Rust, but I do have a fair amount experience with it and I think that much of my Rust knowledge transfers fairly well. I am also excited to get experience working on a large C++ codebase as it is something that I lack knowledge about but would be excellent for future opportunities. In the time that I've been working on appleseed so far, I've already felt myself become acclimated and improve quite a bit.

I would say my proficiency with Git and GitHub are quite good, and I have quite a bit of experience with following coding guidelines that are not mine; that said, in Rust, which is my primary language, we have an awesome and very standardized tool called `rustfmt` which automatically formats code according to project guidelines. So, it might take a bit of getting used to before I stop making small formatting errors, but overall I am proficient in this way.

As far as code reviews, I've had my code reviewed on all the open source projects I've contributed to in the past and have almost always had good experiences with it. I've also reviewed others' code on those projects. Code review just feels natural to me at this point, perhaps becuase of the somewhat nonstandard way that I've learned and participated in programming.

Finally, I would just like to say that I really, really appreciate the way that the appleseed dev-team, Discord, and community in general is managed; you've managed to strike an awesome balance of friendliness and familiarity with professionalism. It's made me feel very welcome and encouraged, and I am very excited to potentially have the opportunity to work with everyone over the summer.

## References

[oit]: http://jcgt.org/published/0002/02/09/
1. [Weighted Blended Order-Independent Transparency (McGuire et.al.)][oit]