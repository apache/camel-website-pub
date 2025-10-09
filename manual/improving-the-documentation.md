# Improving the documentation

The Apache Camel project loves your help with improving the documentation, whether its a tiny typo fix, or adding more details to an existing component, etc.

> **Note**
> This page only describes working with the 'documentation' portion of the website. Other portions are written in Markdown and built using Hugo.

## Simple changes

If there’s an `edit this page` button at the top right of the page, and you wish to propose a simple change such as fixing a typo or rewording something, use this [very simple process](faq/how-do-i-edit-the-website.md). For more complicated changes, including changing xrefs, adding, removing or renaming pages, and significant organizational changes, please use the process described on this page.

## Where to find the documentation

All the documentation accessible in the left-hand navigation panel in the documentation portion of the website is managed in the [AsciiDoc format](https://asciidoc.org/) and built with the [Antora](https://antora.org) static site generator. As of November 2021, by far the most capable AsciiDoc editor is the Intellij AsciiDoc plugin, which works with all Intellij editor products including the free IDEA Community Edition. The plugin preview is more capable than viewing a local AsciiDoc file with a browser plugin as it has some understanding of Antora structure. Note that the only reliable way to preview your changes is with a full build of the Antora portion of the website.

The files have the extension `.adoc` and are managed in the Camel repositories. General documentation is usually directly editable. Component specific documentation is partially or entirely generated from other metadata sources which are in turn generated from the code, often from javadoc. Altering generated documentation requires finding the original source, which varies by project. Editable pages are found in several different places in the repositories:

Main camel repository

Camel components

In the `src/main/docs` folder for the component or camel module. These are symlinked to under `docs/components`.

EIPs

In the `core/camel-core-engine/src/main/docs` folder.

Core languages

In the `core/camel-core-languages/src/main/docs` folder. Note that many languages are under `components`.

User manual and FAQS

In the `/docs/user-manual` folder.

Camel Karaf

In the `docs` folder.

Camel Spring Boot

Most documentation is generated and appended to the component documentation it applies to. Editable pages are under `docs/spring-boot` and `core/camel-spring-boot/src/main/docs` and `core/camel-spring-boot-xml/src/main/docs`.

Other subprojects

camel-k, camel-k-runtime

Under `docs`. There is no generated `camel-k` documentation.

camel-kafka-connector

Editable pages are under `docs`. Most documentation is generated directly from the generated json files for each connector under `connectors/<connector-name>/src/generated/resources`.

camel-kamelets

Only `docs/modules/ROOT/pages/index.adoc` is editable. All other documentation is generated from the kamelet yaml descriptors.

camel-quarkus

Editable pages are under `docs`. Pages under `docs/modules/ROOT/pages/reference/components` and `docs/modules/ROOT/pages/reference/extensions` are generated, including optional snippets from e.g. `extensions/activemq/src/main/doc`.

camel-quarkus-examples

Editable pages are under `docs`.

## How to build the website locally, with your changes

First, make sure you have yarn, version >= 3.1.0, installed globally.

All three builds rely on a 'site-manifest' that lists the contents of the site with enough detail so that Antora knows about all the pages.

> **Note**
> The following procedure is not available in all subprojects yet. If there is no `docs/local-build.sh` in the one you are working on, please ping djencks on zulip and I’ll try to get it in soon.

### Directory layout and initial setup

You need a single directory, such as `camel`, that contains all the camel subprojects you are working with, and the `camel-website` project.

```console
cd camel
git clone https://github.com/apache/camel-website.git
```

### Quick partial build

In your project, run

```bash
./local-build.sh quick
```

This will build your local subproject substituted into the main Camel website build. It will check syntax in your local subproject, and xrefs within it and from it to the rest of the site. It will not check xrefs into your subproject.

Under `camel-website/documentation` you will find only the pages for your subproject. Looking at this in a browser, links within the subproject will stay in the local pages, and links to the rest of the site will go to the main camel site. There is no obvious way to get back to your local pages.

### Full local Antora build

You only have to do this once, and again whenever there are significant changes to the website.

In your project, run

```bash
./local-build.sh full
```

This will build the entire site, including your changes in your branch, and generate a 'site-manifest' listing all the contents of the website, that can be used to build only small parts of the site. This full build will also check that all xrefs into your subproject branch are valid.

### Subsequent partial continuous builds

After this full build completes, you can work on documentation with live updates in your browser by running

```bash
./local-build.sh
```

This will do an initial build of just the current branch in the current subproject, incorporating it into the full site built in the full build, start a web server to serve the site, set up browser-sync on pages you are looking at in your browser, and rebuild the (partial) site as it detects changes. Depending on the amount of content generation Antora is doing, this may take up to a minute or so.

This partial build will detect broken xrefs within your branch and from your branch to the main site, but will not (yet) detect broken xrefs from the rest of the site into your branch. If you rename or remove a page please do a full build or check the PR build carefully for broken xrefs.

### Viewing a full build in httpd

If you do a full build (`yarn build-all` or `yarn build` rather than `yarn build:antora` or use of the `local-build.sh` script in a subproject) and have Docker available locally you can view your build served with httpd by running `local-httpd-in-docker.sh`. This is especially valuable to check redirects set up with `page-aliases`.

## Creating a documentation pull request.

> **Note**
> Simple changes such as typo fixes or rewording can usually be done directly at GitHub after pressing the `edit this page` button at the top left of each page. Note that if the page source starts with a comment that the page is copied or generated this will not work! Please do not use this method if you are changing any xrefs or making significant changes to format; instead follow the procedure below.

1.  Fork/clone the appropriate repository from GitHub and switch to the branch you are working with.
    
2.  Create a branch for your work with a name starting with the original branch name, e.g. `git switch -c main-doc-fix`
    
3.  Edit the `.adoc` sources as needed. Preview your work in the Intellij Asciidoc plugin preview or in a browser with an Asciidoctor extension installed.
    
4.  Do a [local website build with your changes](#_local_build_instructions).
    
5.  Commit and push your work and create a PR in the (sub)project repository.
    
6.  Fork/clone the camel-website repository, and create an appropriate branch, e.g. `git switch -c camel-quarkus-main-456`. The following process will work for any number of doc PRs against any number of source repositories: usually you will have one subproject repo and one branch.
    
7.  Locate the `- url` of the project(s) you are working with in the `antora-playbook.yml` under `sources`, and locate the branch(es) you have altered under that `- url`.
    
8.  Add something like this to the end of the `antora-playbook.yml`:
    
    ```yaml
        - require: '@djencks/antora-source-map'
    #      log_level: trace (1)
          source-map: (2)
            - url: 'https://github.com/apache/camel-kamelets.git' (3)
              mapped-url: 'https://github.com/djencks/camel-kamelets.git' (4)
              branches: (5)
                - branch: main (6)
                  mapped-branch: main-collect (7)
                - branch: 0.6.x
                  mapped-branch: 0.6.x-collect
                - branch: 0.5.x
                  mapped-branch: 0.5.x-collect
    ```
    
    <table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Turning on trace logging will show you in great detail what’s changed from the regular playbook, which can be useful if the build is not doing what you expect.</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>List of source urls to substitute, probably only one.</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>The GitHub URL of the subproject you are working on.</td></tr><tr><td><i class="conum" data-value="4"></i><b>4</b></td><td>The GitHub URL of your fork of the subproject.</td></tr><tr><td><i class="conum" data-value="5"></i><b>5</b></td><td>List of modified branches: probably only one.</td></tr><tr><td><i class="conum" data-value="6"></i><b>6</b></td><td>Name of the branch your PR will merge into.</td></tr><tr><td><i class="conum" data-value="7"></i><b>7</b></td><td>Name of your PR branch.</td></tr></tbody></table>
    
9.  At this point you can test your playbook changes locally by running `yarn build:antora` or `yarn build`.
    
10.  Commit the playbook changes, push to your fork of the `camel-website` repository, and open a PR.
     
11.  If all goes well you will get an email telling you where the Netlify preview is; this is also shown on the PR page.
     
12.  Check for build problems and examine the preview.
     
13.  Upon approval, your content PR will be merged. A `camel-website` PR constructed as described here will not need to be merged and may be closed.
     

## New, renamed, or removed pages

-   Add, rename, or remove the xref for your page in the appropriate nav.adoc file.
    
-   Build the entire website and check for broken xrefs: these will appear as errors in the Antora log output.
    

## Changed xrefs

First, read [A guide to xrefs](#_a_guide_to_xrefs)

-   Build the entire website and check for broken xrefs.
    

## Adding a new component version

See [Updating the website after a release](release-guide-website.md).

## A guide to xrefs

For a general explanation of Antora xref syntax see [the Antora documentation](https://docs.antora.org/antora/3.0/page/xref/). Due to the logical structure of the Camel documentation, xrefs will have a very limited choice of structure.

> **Important**
> A bit of confusion is possible here between Antora components and Camel components. Generally an Antora component corresponds more or less to a Camel subproject, and never to a camel commponent. All the camel components are documented in an Antora component named `components`. In this section the word `component` means an Antora component.

> **Important**
> Antora components may be `distributed` which means that the content comes from more than one place, possibly from different repositories. For instance, the `components` component has content from the main camel repository under the start\_paths `docs/components` and `core/camel-core-engine/src/main/docs` and from the `camel-spring-boot` repository under `components-starter` and `docs/components`. Furthermore, the content may not appear in the normal Antora structure but may be collected from a more maven-project-friendly arrangement with an Antora extension.

### xrefs within an (Antora) component

Generally there will never be a reason to refer from one version of a component to another version. To assure this happens without maintenance issues, leave out the version and component segments from the xref, e.g. in the `components` component

```text
xref{blank}:eips:enterprise-integration-patterns.adoc[]
```

**NOT**

```text
xref{blank}:next@components:eips:enterprise-integration-patterns.adoc[]
```

Do this no matter how many locations the component is distributed over.

A xref within the same module can leave out the module segment, although it does no harm.

Do not specify the component name: if you do, the link will be to the `latest` (non-prerelease, i.e., non-`next`) version, not the current version.

### Links to the user manual

The user-manual component is [unversioned](https://docs.antora.org/antora/3.0/component-with-no-version/). Leave out the version segment. For example, this will link to this page from anywhere in the documentation:

```text
xref:manual::improving-the-documentation.adoc[]
```

### Links between subprojects

Each camel subproject relates to other subprojects, and each version of a subproject relates to specific versions of these other subprojects. These subproject versions are specified in the `antora.yml` component descriptor for the documentation component for that subproject. Note that for distributed components each start path has a component descriptor but only one has the additional `asciidoc/attributes` key. For example,

```yaml
name: camel-kafka-connector
title: Camel Kafka Connector
version: next
prerelease: true
display-version: Next (Pre-release)

nav:
- modules/ROOT/nav.adoc

asciidoc:
  attributes:
    camel-version: 3.12.x
    camel-k-runtime-version: 1.8.0
    camel-k-version:
    camel-kamelets-version: 0.3.0
```

> **Note**
> Setting these up is WIP

Use these attributes to refer to documentation for the related subproject, e.g.

```text
xref{blank}:{camel-version}@components:eips:enterprise-integration-patterns.adoc[]
```

If there’s a missing attribute, please raise an issue rather than using a concrete version.