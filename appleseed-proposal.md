# [Light Paths Visualization](https://github.com/appleseedhq/appleseed/wiki/List-of-Project-Ideas-for-GSoC-2019#project-10-improve-light-paths-visualization) and Viewport Unification Proposal

## Contact Information

Gray Olson

- Email: [gray@grayolson.com](gray@grayolson.com)
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

As described in the original project idea description, the first step will be verifying that the current implementation is correct and annotating it with physical properties. Concurrently, I'll be interacting with appleseed and potentially other community members to determine which other quantities would be useful to have the option of recording. These should also be configurable in the renderer, as sometimes we might not want to record all of them.

## Viewport Details

## Light Path Visualization Details

## Project Schedule

I will be on summer break from May 1st to August 22nd. I will be out of town from May 1st to May 12th, but will have my computer with me and will still have a significant amount of time to work on things during that time. In addition, there is a possibility of me doing part time work for a couple of weeks in June, however I don't expect this to interfere with my GSoC participation. In addition, I might go out of town for a week or two in July, but I will have my computer with me and still be able to work full time on GSoC while I am out of town.

### Community Bonding

#### Until May 6

- Actively contribute and push my current PRs through to merging

#### Until May 13

- Get more familiar with Qt
- Get familiar with appleseed's render pipeline

#### Until May 27

- Begin to collect feedback on which additional quantities would be helpful to collect 

## Phase 1

## Phase 2

## Wrap-up

- Final Evaluation
- Final report modifications

## Bio

## References

## Links