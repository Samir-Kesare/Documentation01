# GitFlow Branching Strategy



| Author           | Created on  | Last Updated | Document Version |
|------------------|-------------|--------------|-------------------|
| Khushi Malhotra | 16-01-2024  | 18-01-2024   |        v1          |

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Table of Contents
- [Introduction](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#introduction)
- [Purpose](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#purpose)
- [Key benefits](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#key-benefits)
- [How it works](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#how-it-works)
- [Advantages and Disadvantages](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#advantages-and-disadvantages)
- [Conclusion](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#conclusion)
- [Contact Information](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#contact-information) 
- [Resources and Reference](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Gitflow.md#resources-and-references)
***
![image](https://github.com/avengers-p7/Documentation/assets/156056460/48e501b0-c7f1-44cb-9893-593840731d61)
# Introduction
Gitflow is an alternative Git branching model that involves the use of feature branches and multiple primary branches. It was first published and made popular by Vincent Driessen at nvie. 
Gitflow can be used for projects that have a scheduled release cycle and for the DevOps best practice of continuous delivery.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Purpose
Gitflow is a branching model for Git that aims to streamline the release management process and enhance collaboration within development teams. It achieves this by defining a clear structure and set of rules for how different branches should be used and interacted with.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Key Benefits
| Key Benefit                       | Description                                                                                                     |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Organized Release Management**     | Separates development from release preparation, ensuring a stable main branch.                                  |
|                                       | Facilitates parallel development of features and hotfixes without disrupting the main codebase.               |
| **Improved Collaboration**            | Provides a consistent framework for developers to work within, reducing confusion and conflicts.               |
|                                   | Encourages code reviews and testing before merging into main branches.                                          |
| **Clear History and Traceability**    | Maintains a well-defined history of changes, making it easier to track feature development, hotfixes, and releases. |
|                                   | Simplifies rollbacks if necessary.                                                                              |

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# How it works
![image](https://github.com/avengers-p7/Documentation/assets/156056460/107f133e-c15e-4c9b-9c7f-a0759e6b2dfa)


## Here's a breakdown of the diagram:

| Branch           | Purpose                                                | Origin                 | Merged Into                                            |
|------------------|--------------------------------------------------------|------------------------|--------------------------------------------------------|
| Main Branch      | Represents stable, production-ready code.              | -                      | -                                                      |
|                  | Reflects what is deployed in production.               | -                      | -                                                      |
| Develop Branch   | Integration branch for ongoing development.            | Main Branch            | Main Branch                       |
|                  | New features are implemented and tested here.         | -                      | -                                                      |
| Feature Branches | Created for developing specific features.             | Develop Branch         | Develop Branch                                         |
|                  | Branched off from the develop branch.                 | -                      | -                                                      |
|                  | Merged back into the develop branch upon completion. | -                      | -                                                      |
| Release Branch   | Created when preparing for a new release.             | Develop Branch         | Main Branch and Develop Branch                          |
|                  | Used to stage and test the release.                   | -                      | -                                                      |
|                  | Bug fixes and last-minute features added here.       | -                      | -                                                      |
|                  | Merged into both main and develop branches.           | -                      | -                                                      |
| Hotfix Branch    | Created to address critical issues in production.     | Main Branch            | Main Branch and Develop Branch                          |
|                  | Branched off from the main branch.                    | -                      | -                                                      |
|                  | Merged into both main and develop branches.           | -                      | -                                                      |


## Here are some additional details about the Git flow workflow

| **Pull Requests** | **Versioning** | **Deployment** |
|-------------------|-----------------|-----------------|
| Developers should create pull requests to merge their changes from feature branches into the develop branch. This allows for code review and testing before the changes are merged. | Releases are typically tagged with a version number. This makes it easy to track which changes are included in each release. | The specific way that releases and hotfixes are deployed to production will vary depending on the project. |

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Advantages and Disadvantages
| **Advantages of Gitflow**                                       | **Disadvantages of Gitflow**                                |
|------------------------------------------------------------------|-----------------------------------------------------------|
| Clear and organized branching structure: Makes the development process more transparent and easier to understand for the team. | Can be complex for small teams: The multiple branches and workflow can be cumbersome for small teams with simple projects. |
| Promotes stable releases: Isolates feature development and hotfixes from the main branch, minimizing the risk of introducing instability. | Potential for bottlenecks: Code reviews and merges can create bottlenecks if not managed effectively. |
| Enables parallel development: Different features can be worked on simultaneously without disrupting the main codebase. | Less suited for rapid release cycles: Frequent releases may cause merge conflicts and slow down the process. |
| Provides clear versioning: Releases are tagged with version numbers, simplifying release management and tracking. | Overhead for release tasks: Release branches require additional work for packaging and deployment. |
| Encourages code reviews and testing: Pull requests ensure code quality before merging to the main branch. | Not ideal for continuous integration: The focus on separate branches can clash with a continuous integration approach. |

-------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Conclusion
Gitflow, while powerful, isn't a one-size-fits-all solution. Its structured approach shines in large projects with defined release cycles, but its complexity can burden smaller teams or those needing frequent releases. Consider alternative workflows for agility and simplicity, prioritizing Gitflow only if control, organization, and predictable launches are top priorities.
***
Some other alternatives of GitFlow are:- 
- [Environment Branch](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/Env%20branch.md)
- [Feature Branch](https://github.com/avengers-p7/Documentation/blob/main/VCS/Design/FeatureBranch.md)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Contact Information
| Name            | Email Address                        |
|-----------------|--------------------------------------|
| Khushi Malhotra | khushi.malhotra.snaatak@mygurukulam.co |

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Resources and References

| Resource                                  | Content                                                      |
|-------------------------------------------|--------------------------------------------------------------|
| [Git Flow Documentation](https://medium.com/@matt_weingarten/version-control-done-right-with-gitflow-8623eb051ea2) | Introduction, Gitflow                                       |
| [Atlassian Git Flow Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) | Diagram, How it works, Types of branches                    |
| [Advantage & Disadvantage](https://medium.com/@ferrohardian/git-flow-pros-and-cons-85b398a64848) | Advantage and disadvantage of git flow                      |

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
