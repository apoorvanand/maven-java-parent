Frequently Asked Questions
----

It can be unsettling having a new parent POM introduced into a development process where one did not previously exist.
It can lead to a number of questions, for which it is hoped the following FAQ may answer. For all other questions,
please feel free to contact [jonathan.giles@microsoft.com](mailto:jonathan.giles@microsoft.com) in the first instance.

#### What exactly is going on here?

The intent is to introduce a common 'bill of materials' (BOM) across all Microsoft Java SDKs. This BOM may also be
referred to as a 'parent POM' or 'super POM'. This project ships, at present, two parent POMs, one for Java 8, and one 
for Java 11, although all focus at present is on the Java 8 POM.

A parent POM lists a large number of dependencies, including their Maven `groupId`, `artifactId`, and most importantly, their 
`version`. When individual SDK projects depend on this parent POM, they no longer have to specify the version number for
their dependencies, as these will instead be inferred from the parent POM. This means that all projects that depend on
this parent POM, assuming they specify no versions in their own POM files, will be consistently using the same version.

#### But doesn't using the parent POM mean we get a huge number of dependencies in our project?

No. The parent POM does indeed have more dependencies listed in it - it is the superset of all dependencies for all
children project after all - but this does not mean that all dependencies are added to your project. You should think
of the parent POM as simply a map of (Maven groupID + Maven artifactId) to Maven version number, and nothing more.

#### What if I need to add a new dependency, and it isn't listed in the parent POM?

Submit a pull request to this repo, with the new dependency added to the relevant POM file (Java 8 or Java 11). While
you are waiting for this to be accepted, you can feel free to add the version number to your own POM - but please be
conscious of this and remove it at your earliest convenience (i.e. when the PR is merged and the new parent POM released).

#### Why are we doing this?

Because at present each Azure SDK manages its own dependencies, and these can often conflict with the dependencies of
other Azure SDKs. This causes what is commonly referred to as 'classpath hell' for our users. While our individual SDKs
may all work well, when they are brought together by an end user, they can be found to not operate well (or at all) with
each other.

#### Who should be using this parent POM?

It is  intended for this parent POM to be used only by engineering teams at Microsoft to ensure consistency of 
dependencies. In the future, Microsoft may ship outside-facing BOMs that perform a similar function to this parent POM,
but instead specify versions of our Java SDKs that are known to work together. This can be known because we would
require that all elements listed in this outside-facing BOM to have the same version of this parent POM. 

#### What if I need a different version of a dependency than what is listed in the parent POM?

The process for updating versions is to use GitHub pull requests, and to centralise discussion within that pull request. 
There will be a representative from each team currently consuming the parent POM included in the CODEOWNERS file, so that
all pull requests have them as code reviewers and as such notified of incoming proposals. 

We will have a 72 hour time window for any dissenting opinions, after which time the pull request will be merged. If 
there is a disagreement, the discussion will happen in the GitHub pull request as to why, and how to proceed.

#### What if I urgently need to upgrade a dependency?

If you urgently need to upgrade a dependency, you should still communicate with this team to ensure knowledge is shared, 
and that plans to move to this new version can begin, but you should not feel as if you cannot do you what you must do.
You can specify a version in your projects POM for that specific version, but please treat it as if it is a short-term
solution, and try to ensure that you return back to the centralised versioning for all dependencies as soon as possible.

#### What if a dependency is found to have a security issue or other concern?

There may be rare times when a dependency in this parent POM is urgently needing to be upgraded, due to a security
vulnerability being found, for example. Depending on how critical the issue is, there is a guarantee that communication
will continue to happen in the standard process, however there may already be a commit and a new parent POM version
ready for all SDK teams to upgrade to. 

Because this new parent POM will have an updated version number, it will not impact any processes for child projects, as 
they will still depend on the previous release. Depending on how critical the issue is, the team responsible for 
maintaining this parent POM may also submit pull requests into all SDK repos to ensure they are updated to the new
version.

#### What happens when a pull request modifies the parent POM?

A build will be kicked off that will result in the parent POM being published to Maven Central. All teams making use of
the parent POM will need to update to the latest version in their respective repositories.

#### How important is it to remain on the latest version of the parent POM?

Ideally, all teams would be automatically updated to the latest version to ensure consistency. However, it is conceivable
that teams could lag to a certain extent without issue. The only time it is important to ensure that the version is the
latest version of the parent POM is right before any release of the SDK. If this is ensured, then we can be assured
that if / when a outside-facing BOM is released, that all versions listed there are consistently on the same parent POM.

#### What is our shared dependency versioning plan?

We do not intend to 'lead the pack' and always update to the latest version of all dependencies. We will instead be
fast followers and keep ourselves informed of where the wider Java community stands on versioning.