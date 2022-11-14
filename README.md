# mps-gradle-scripts

This repo contains helper gradle-scripts to download MPS, plugins and related JBR directly from the official MPS-URLs.

It is intended to copy the related files into your own repo, or include them by URL.

## Setup new Project

* create a new directory for your project (e.g. `mps-gradle-setup-sample/`)
* copy files/directories 
  - folders `.github`, `gradle`
  - files `build.gradle`, `build.xml`, `gradle.properties`, `gradlew`, `gradlew.bat`
* adapt `build.gradle`
  - modify `ext.mpsVersion`: change to desired MPS version
  - modify `ext.mpsPlugins`: change necessary MPS plugins
  - modify `ext.languageName`: change to language name (e.g. `MySetupSampleLanguage`)
* execute `gradlew prepareMps`
* execute `gradlew openProjectInMps` to open the downloaded MPS with installed plugins
  - note: ensure that no other MPS instance is running
* in MPS: create a new project
  - set project name (e.g. `MySetupSample`)
  - set project location to your project directory (e.g. `<path-to-projects>\mps-gradle-setup-sample`)
  - set language name (e.g. `MySetupSampleLanguage`)
* in MPS: create a new build module
  - right click on project: `New/Build Solution`
  - take suggested name (e.g. `MySetupSample.build`) and proceed wizard
  - modify the build model
    * change the `macros` section to this:

      ```
      folder mps_home = ./build/mps-bundle/mps 
      folder project_home = . 
      folder mps.macro.project_home = $project_home
      ```
    * change the `zip` archive name of the `default layout` section to the language name (e.g. to `MySetupSampleLanguage.zip`)
      - this is necessary if language-name != project-name
* execute `gradlew downloadGithubActionsScripts`
  - this re-downloads the github-action scripts and replaces the placeholders
* execute `gradlew mpsBuild`
  - this should build the archive "build/artifacts/<projectName>/<projectName>.zip" successfully

## Integrate into existing Project

* have a look on sample project (below)
* also look at the steps above, which deal with the build-script related files

## Update gradle scripts

* when properly set up, we have a file `gradle/init-gradle-scripts.gradle`, which contains tasks to update the gradle scripts from the base repository:
  - `downloadGradleScripts`: re-downloads the gradle scrips under `gradle/*`
  - `downloadGithubActionsScripts`: re-downloads the GitHub Actions files under `.github`
* Note: ensure you commit before executing this tasks, since they overwrite the files
  - usually, you should not modify the base scripts at all

## Example repositories

* https://github.com/vimotest/viewmodel-testlang-prototype
* https://github.com/Fumapps/mps-gradle-setup-sample
