# Updating the website after a release

Most steps are the same for all releases, although some details may vary. There are several cases:

-   A single repository release, such as `camel-kafka-connector`.
    
-   A set of separately versioned repositories, such as `camel-k`, `camel-k-runtime`, and `camel-kamelets`.
    
-   The set of main `camel` and `camel-spring-boot` which are versioned together.
    

Changes in the content repositories may be done as part of release preparation, or later. Changes in the `camel-website` `antora-playbook.yml` can be supplied in a PR at any time but should be merged only after the release is voted on and approved.

We’ll use the notation `<repo short name>:<path>` to indicate the file to be changed. For instance, `camel:docs/components/antora.yml` for the `docs/components/antora.yml` component descriptor in the main camel repository, in whatever branch is under discussion.

## After the new release, branches are created in all affected content repositories

These will always be branches from `main`. Changes to all the new branches, e.g. `camel-3.13.x`, will be necessary. The changes are almost the same whether the new branch is LTS or not.

### Changes to the new branches (e.g. `camel-3.13.x`) in affected content repositories

1.  Examine the `content:sources` key of the `camel-website:antora-playbook.yml` and locate the URLs of the repositories.
    
2.  For each URL, locate the `start_path` or `start_paths` key.
    
3.  For each start path entry, locate the `antora.yml` component descriptor at that path in the new branch in the repository. For each Antora component, exactly one of the associated component descriptors will have additional information beyond the name and version. The version will need to be updated in all associated component descriptors, and the additional information only in the one containing it. The primary component descriptor, having been duplicated from `main`, will specify version `next` and related properties, and will look something like this:
    
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
        camel-kamelets-version: 0.3.0
        prerelease: true
    ```
    
4.  Set the version to the documentation version for the new release, e.g. `0.11.0`.
    
5.  Remove the top level `prerelease` key.
    
6.  If the new release is LTS, set the `display-version` appropriately, e.g. `0.11.0 (LTS)`: otherwise remove the `display-version` key.
    
7.  Consider the versions listed in `asciidoc/attributes`. These represent the other camel subprojects this one depends on.
    
    -   For subprojects outside the current release set, these will not change on release.
        
    -   For subprojects in the same release set, such as `camel` and `camel-spring-boot`, these versions will need to be updated to refer to the new version of the other subproject.
        
    
8.  Remove `prerelease` from `asciidoc/attributes`.
    
9.  If the release is LTS, add an `lts` attribute specifying the date out of service.
    
10.  Find the `source-map.yml` file next to the `antora.yml` component descriptor. It will look something like this:
     
     ```yaml
         - require: '@djencks/antora-source-map'
     #      log_level: trace
           source-map:
             - url: 'https://github.com/apache/camel-kamelets.git'
               mapped-url: './../camel-kamelets'
               branches:
                 - branch: main
                   mapped-branch: HEAD
     ```
     
     Change the `- branch: main` to specify the branch being released, e.g. `- branch: 0.6.x`.
     
11.  Build each project (e.g. `mvn clean install -Pfastinstall`) and check for generated changes that need to be committed (or undone if there are tooling problems).
     
12.  There will also be `local-build.sh`, `source-map.yml`, and `source-watch.yml` files in the docs directory of the subproject. These files support [local partial builds of the subproject](improving-the-documentation.html#_local_build_instructions). In `source-map.yml`, change the `branch` value from `main` to the new git branch name for the release.
     

Since the branches with these changes have not yet been added to the Antora playbook, they may be kept on a PR fork/branch or merged into the release branch locally or in the repository.

### Playbook changes

These changes must go through a PR before being merged, and it is highly advisable to build the website locally to check for problems.

1.  As in the previous section, examine the `content:sources` key of the `camel-website:antora-playbook.yml` and locate the URLs of the repositories.
    
2.  Under `branches` add the new branch directly under `main`, so the branches appear in reverse chronological order, newest first. Note that this is the git branch name, which is related to but usually not identical to the Antora component version.
    
3.  Consult these [local build instructions](improving-the-documentation.html#_local_build_instructions).
    
4.  Consult these [instructions for creating a documentation PR](improving-the-documentation.html#_creating_a_documentation_pull_request). Note that your `camel-website` PR will definitely need to be merged after removing the `source-map` extension configuration used to preview the website changes.
    

### Notes for specific projects

#### camel-quarkus

Many of the versions in the `antora.yml` component descriptor are set by the maven build from `pom.xml` properties. Check that these have appropriate values after running the build. If the build sets inappropriate values, consider fixing or disabling the groovy script.

## Removing obsolete component versions

After each release, it may be possible to remove old versions of the documentation from subprojects. This depends on whether any current versions of other subprojects depend on the old subproject versions.

The experimental approach is to remove the old branches from the playbook and build the site. If there are errors from broken xrefs pointing to the removed version, put them back.

You can also examine the component descriptors of older versions of subprojects that depend on the current subproject, but it is not obvious how to determine which these are without looking at all of them.