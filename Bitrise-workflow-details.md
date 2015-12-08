Here's the deal with Bitrise. 

1. As of [`f59d4ba`](https://github.com/mapbox/mapbox-gl-native/commit/f59d4ba920bcd132a9e0841a993f1559d96fd480) (already in `master`), the config for running through our steps for Bitrise has been moved out of their GUI workflow builder and into [`bitrise.yml`](https://github.com/mapbox/mapbox-gl-native/blob/f59d4ba920bcd132a9e0841a993f1559d96fd480/bitrise.yml) in the repo root (for whatever branch). 

1. The Bitrise config for the repo has been set to just run the relevant branch's `bitrise.yml`. 

1. If you want to change the `bitrise.yml`, do so and use the `bitrise` CLI tool (`brew install bitrise` or [manual install](https://github.com/bitrise-io/bitrise/releases)) to `bitrise validate`. 

1. Change the [`primary`](https://github.com/mapbox/mapbox-gl-native/blob/f59d4ba920bcd132a9e0841a993f1559d96fd480/bitrise.yml#L17) workflow in your branch to see how changes will be run on Bitrise before merging them to `master`, affecting all branches (since all branches run their respective `primary` workflow). You can create alternate workflows, named after branches, to have them run by commits in that branch, but generally we will just use `primary`. 

1. You can also create custom non-branch-related workflows in the `bitrise.yml` beyond the default `primary` one, such as eventually where we will have a `roll_build` or similar workflow to address [#2844](https://github.com/mapbox/mapbox-gl-native/issues/2844). 

1. Both `[skip ci]` and `[ci skip]` anywhere in commit messages work for our Bitrise setup for this repo as of [`f5bb746`](https://github.com/mapbox/mapbox-gl-native/commit/f5bb746f6a3e68268c23125ca7acdf549a9cacda). 

More on Bitrise's steps library (for example, we use the `select-xcode-version`, `script`, `xcode-test`, and `slack` steps): https://github.com/bitrise-io?utf8=✓&query=steps and http://www.steplib.com