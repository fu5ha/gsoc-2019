# [Light Paths Visualization](https://github.com/appleseedhq/appleseed/wiki/List-of-Project-Ideas-for-GSoC-2019#project-10-improve-light-paths-visualization) and Viewport Unification Proposal

## Contact Information

Gray Olson

- Email: [gray@grayolson.com.com](gray@grayolson.com)
- Discord: *Fusha#8156*
- GitHub: [termhn](https://github.com/termhn)

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
2. Light paths report/summary creation
    * Have some basic built-in, configurable data analysis that could provide a summary of collected data about a group of light paths. i.e. number of rays above a certain radiance threshold, with certain hue, etc.

## Light Path Recording Details

As described in the original project idea description, the first step will be verifying that the current implementation is correct and annotating it with physical properties. Concurrently, I'll be interacting with appleseed and potentially other community members to determine which other quantities would be useful to have the option of recording.

### Tests / Optimization

- Test if the rendered images are correct
- Observe how pixels are sampled
- Reduce memory use if possible
- Port the implementation on multiple threads if originally implemented on a unique thread

## Project Schedule

I will have vacations from May 25 to August 31, which leaves a bit more time than planned. I will be able to work completly on this project during this period. I will also be available before May 25 because most of my units would have been finished by then. Here is an estimation of the project schedule:

### Community Bonding

#### Until May 14

- Actively contribute
- Get familiar with appleseed's render pipeline
- Get familiar with blenderseed

### Adaptive Sampling

#### Week of May 14

- List all methods that can be implemented directly into appleseed and the one that requires a fair amount of refactoring
- Compare methods between each other
- End of the week, along with maintainers: **Decide which solution will be implemented**

#### Week of May 21

- Get familiar with the chosen method 
- Outline the algorithm
- Produce diagrams of what the final code structure would be
- Propose an interface for configuring the sampler
- Discuss of the structure with maintainers

#### Week of May 28

- Naive implementation of the algorithm
- Refactor appleseed if needed to fit the new sampler
- Create some test scenes
- Use diagnostic AOVs to observe the results

#### Week of June 4

- Continuing previous week tasks

#### Week of June 11: End of phase 1

- Evaluation of the Phase 1
- Preparation for Phase 2
- Work on the final report

#### Week of June 18

- Test the naive implementation
- Fix issues (there will be some :smile:)
- Improve previously create diagrams if needed
- Test the algorithm on animations

#### Week of June 25

- Optimize the algorithm
- Optimize memory management

#### Week of July 2

- Better integration of the sampler inside source code
- Add the new sampler in appleseed.studio

#### Week of July 9: End of phase 2

- Evaluation of Phase 2
- Preparation for Phase 3
- Work on the final report
- Compare results with the original adaptive sampler
 
#### Week of July 16

- Test again with the same scenes as before
- Remove the original adaptive sampler
- Final fixes, tests and documentations

### Resumable Renders

#### Week of July 23

- Find how to interrupt renders
- List things that need to be saved to resume the render
- Implement a current rendering-state saver
- Implement interruption and use the previous file saver

#### Week of July 30

- Allow to restart a render from appleseed.cli

#### Week of August 6

- Final Evaluation
- Final report modifications

## Bio

I am 21, studying *Compute Science and Image Science* at the University of Strasbourg, France, currently in the first year of a Master's Degree. Computer graphics and especially rendering fascinate me, I am doing my best for being ready to enter the industry. I have experience with NPR and real-time rendering, and I am learning about physically based renderers. I have professional experience with Python, which I acquired by working in 2 different animation studio (one in Luxembourg named *La Fabrique d'Images* and one in Paris named *Ellipsanime*). Developing tools for artists was my principal task. Thanks to school and personal projects, I have advanced knowledge of C++ and C. Also, I am starting to get comfortable with Scientific Papers as I am using them to implement school projects.

## References

- [A Hierarchical Automatic Stopping Condition for Monte Carlo Global Illumination](https://jo.dreggn.org/home/2009_stopping.pdf)

## Links

- [Adaptive Sampling by Yining Karl Li](https://blog.yiningkarlli.com/2015/03/adaptive-sampling.html)
- [Final Project Report by Benedikt Bitterli](http://noobody.org/is-report/medium.html)