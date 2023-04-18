# How to contribute

F3D welcomes all contributors, regardless of skill level or experience!

## Contributing as a user

To contribute to F3D as a user, you can just use F3D and report any issues or feature ideas.
Please open your own issue to share any issues or ideas you may have, and comment on any related issues.

Also, do not hesitate to join our [discord](https://discord.f3d.app) !

## How to get started with development

To contribute to F3D as a developer, you may want to take a look at the opened [issues](https://github.com/f3d-app/f3d/issues),
especially, the ones with the ["good first issue"](https://github.com/f3d-app/f3d/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) label.
If one sounds interesting to you, then you should just go ahead and comment on the issue and ask for any help or clarification needed.
F3D maintainers will see your comment and provide guidance as needed.

You can then fix the issue in your side and contribute it to the F3D repository,
by following the workflow described below.

Another way to get started is to improve the documentation.

## F3D Development workflow

F3D uses the [gitlab flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html). In a few words, here is how to contribute:
- [Fork](https://github.com/f3d-app/f3d/fork) F3D repository on github.
- Create and push a feature branch on your fork containing new commits.
- When it is ready for review or when you want to run the CI, create a pull request against `f3d-app/f3d/master`.
- Once the PR is approved and CI comes back clean, a F3D maintainer will merge your pull request in the master branch
- The master now contains your changes and will be present in the next release!

## Continuous Integration

F3D has a pretty extensive continuous integration trying to cover all usecases for F3D.
It means that if your change break the CI in your PR, it will not be merged until the breaking change are addressed.
It also means that adding a new feature or behavior means adding a associated test.
Make sure to check the results for yourself, and ask for help if needed.

F3D continuous integration will also check the coverage as it is a good way to evaluate if new features are being tested or not.
When adding code to F3D, always to to cover it by adding/modifying [tests](TESTING.md).

F3D continuous integration also check formatting using clang-format and will inform you if changes needs to be made.
However, some [formatting rules](CODING_STYLE.md) are not enforced by clang-format and will be checked during the review process.

When making changes to the libf3d public API, the CI will warn about making related changes to the bindings. This is required in order to merge the PR.

## F3D architecture

F3D is separated in different components:
- The F3D application, in the application folder.
- The libf3d, in the library folder.
- The VTKExtensions in the library/VTKExtensions folder.
- The bindings, python, java and webassembly, in the respective directories.
- The plugins, providing all the different readers in the plugins directory.

VTKExtensions are separated in different modules.
- Core, that do not depend on any other VTKExtensions modules are provide services for all modules
- Readers, that depends on Core and implements many new VTK readers and importers
- Rendering, that depends on Core and implements the rendering specificities of F3D
- Applicative, the depends on all other VTKExtension modules and provide services for the libf3d library

The libf3d implements the whole logic of instancing and manipulating the different VTK classes, it is fully documented [here](../libf3d/README.md).

The F3D application itself uses the libf3d but adds an applicative layer on top of it, especially the handling of [command line options](../OPTIONS.md)
and [configuration file](../CONFIGURATION_FILE.md).