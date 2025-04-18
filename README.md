# Header Remapping with Swift PM

This is a minimum reproducer to show that is not possible to remap headers using Swift PM.

## Motivation
We are working on migrating React Native away from Cocoapods to Swift Package Manager (Swift PM).

React Native is 10 years old and it is a mixture of C++, Objective-C and Objective-C++.

One of the problem that we have is that our import/include statement and our folder structure is not standard. We have a folder named `React`, where all the Objecitve-C/C++ code is located. The React folder contains several subfolders which may contains source files or other subfolders.

To exaplain the problem, I created this repo which reflect one of this use cases.
The `Dependency` folder has a `Root` folder and a `Subfolder`. The `Subfolder` contains a C++ object named `MyObject`. The header is `MyObject.h` and the implementation is `MyObject.cpp`.

The `App` folder contains an executable, which we want to include the `MyObject` object using the `#include <Root/MyObject>` include path, effectively skipping the `Subfolder` path.

This works with Cocoapods because it allows to remap where the headers must be located. However, Swift PM does not have the same feature.

I also tried to use a custom module map, but the custom module map is never picked up by Swift Package Manager. When I explore the `.swiftpm` folder, I only find the automatically generated `module.modulemap` which content is different from what I specified.
