<!-- @head-content@ -->
# laplacian/domain-model.project-template

This is a template module that generates directory structure, development scripts, and relating documents for a domain model project.


*Read this in other languages*: [[日本語](README_ja.md)] [[简体中文](README_zh.md)]
<!-- @head-content@ -->

<!-- @toc@ -->
## Table of contents
- [Overview](#overview)

  * [Model overview](#model-overview)

- [Usage](#usage)

- [Index](#index)

  * [Entity list](#entity-list)

  * [Script List](#script-list)

  * [Source code list](#source-code-list)



<!-- @toc@ -->

<!-- @main-content@ -->
## Overview


### Model overview


The following diagram explains the entities included in this module and the relationship
between them.
![](./doc/image/model-diagram.svg)

## Usage

To apply this Template module, add the following entry to your project definition.
```yaml
project:
  templates:
  - group: laplacian
    name: domain-model.project-template
    version: 1.0.0
```

You can run the following command to see a list of resources affected by the application of this module and their contents.
```console
$ ./script/generate --dry-run

diff --color -r PROJECT_HOME/.NEXT/somewhere/something.md PROJECT_HOME/somewhere/something.md
1,26c1,10
< content: OLD CONTENT
---
> content: NEW CONTENT
```

If there is no problem, execute the following command to reflect the change.
```console
$ ./script/generate

```


## Index


### Entity list


- [**Document**](<./doc/entities/Document.md>)
document
- [**DocumentLanguage**](<./doc/entities/DocumentLanguage.md>)
document_language
- [**Section**](<./doc/entities/Section.md>)
section
- [**Module**](<./doc/entities/Module.md>)
module
- [**ModuleRepositoryList**](<./doc/entities/ModuleRepositoryList.md>)
module_repository_list
- [**Project**](<./doc/entities/Project.md>)
project
- [**ProjectType**](<./doc/entities/ProjectType.md>)
project_type
- [**Script**](<./doc/entities/Script.md>)
script
- [**Option**](<./doc/entities/Option.md>)
option
- [**SourceRepository**](<./doc/entities/SourceRepository.md>)
source_repository
- [**LocalizedText**](<./doc/entities/LocalizedText.md>)
localized_text
- [**MultilingualText**](<./doc/entities/MultilingualText.md>)
multilingual_text
- [**NamedParam**](<./doc/entities/NamedParam.md>)
named_param
- [**NamedValue**](<./doc/entities/NamedValue.md>)
named_value
### Script List


- [./script/generate.sh](<./scripts/generate.sh>)

  Generates the resources in each directory of `src/` `model/` `template/` in this project.
  The results are reflected in each directory of `dest/` `doc/` `script/`.

  *Generator input files*

  - `src/`
    Stores static resources that are not processed the generator.
    The contents of this directory are copied directly into the `dest/` directory.

  - `model/`
    Stores the static model data files written in *YAML* or *JSON* format used for the generation.

  - `template/`
    This directory contains the template files used for the generation.
    Files with a extension `.hbs` will be handled as templates. All other files are copied as is.

    - `template/dest` `template/doc` `template/scripts`
      Each of these directories contains the template files of the resource to be output
      in the directory `dest/` `doc/` `scripts`.

    - `template/model` `template/template`
      These directories store template files updating the contents of `template/` and `model/` used for the generation.
      If the content of `template/` `model/` is updated as a result of the generation,
      the generation process is executed recursively.
      The changes to `template/` `model/` that occur during the above process are treated as an intermediate state
      and will be lost after the completion of the process.
      Use the *--dry-run* option to check these intermediate files.

  *Generator output files*

  - `dest/`
    Outputs the source files of applications and modules created as the result of
    the generation process.

  - `doc/`
    Outputs the project documentation.

  - `scripts/`
    Outputs various scripts used in development and operation.

  > Usage: generate.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -d, --dry-run
  >
  >   After this command is processed, the generated files are output to the `.NEXT` directory
  >   without reflecting to the folders of `dest/` `doc/` `scripts/`.
  >   In addition, the difference between the contents of the `.NEXT` directory and the current files.
  >   This directory also contains any intermediate files created during the generation.
  >   
  > -r, --max-recursion [VALUE]
  >
  >   The upper limit of the number of times to execute recursively
  >   when the contents of the `model/` `template/` directory are updated
  >   during the generation process.
  >    (Default: 10)
- [./script/publish-local.sh](<./scripts/publish-local.sh>)

  After the resources in the project are generated,
  the resources in the `./dest` directory are built as a template module
  and registered in the local repository.

  > Usage: publish-local.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -r, --max-recursion [VALUE]
  >
  >   This option is the same as the option of the same name in [generate.sh](<./scripts/generate.sh>).
  >    (Default: 10)
  > , --skip-generation
  >
  >   This option is the same as the option of the same name in [generate.sh](<./scripts/generate.sh>).
  >   
### Source code list


- [model/project.yaml](<./model/project.yaml>)
- [src/{if entities}doc/entities/{each entities.in_namespace as entity}{entity.class_name}.md.hbs](<./src/{if entities}doc/entities/{each entities.in_namespace as entity}{entity.class_name}.md.hbs>)
- [src/{if entities}doc/image/model-diagram.puml.hbs](<./src/{if entities}doc/image/model-diagram.puml.hbs>)
- [src/model/project/document/sections/{if entities}/index/entity-list.hbs.yaml](<./src/model/project/document/sections/{if entities}/index/entity-list.hbs.yaml>)
- [src/model/project/document/sections/{if entities}/overview/model-overview.hbs.yaml](<./src/model/project/document/sections/{if entities}/overview/model-overview.hbs.yaml>)
- [src/model/project/{if project.domain_model}subprojects/{project.group}.{project.name}-plugin.hbs.yaml](<./src/model/project/{if project.domain_model}subprojects/{project.group}.{project.name}-plugin.hbs.yaml>)


<!-- @main-content@ -->