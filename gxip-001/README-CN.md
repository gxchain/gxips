    GXIP: 0001
    Title: GXChain改进提案目的和指南
    Authors: David Lan <lanhaoxiang@gxb.io>
    Status: Draft
    Type: Informational
    Created: 2018-11-07

# 什么是 GXIP?

GXIP代表GXChain改进提案，但也可以视为改进协议。 GXIP是一个设计文档，向GXChain社区提供信息，或描述GXChain或其流程或环境的新功能。 GXIP应提供有关特征或想法的简明技术规范及其理由。它不仅可以描述技术改进，还可以记录最佳实践和建议。

我们打算将GXIPs作为提出新功能，收集社区对问题的意见以及记录GXChain设计决策的主要机制。 GXIP作者负责在社区内建立共识并记录不同意见。

由于GXIP在版本化存储库中作为文本文件维护，因此其修订历史记录是功能提议的历史记录。

# GXIP有哪些类型

GXIP分为两种：

* **信息类GXIP**描述GXChain设计问题，或向GXChain社区提供一般指南或信息，但不提议新功能，协议更改或任何其他修改。信息类GXIP不一定代表GXChain社区的共识或建议，因此用户和实施者可以自行选择是忽略信息类GXIP还是遵循他们的建议。比如*最佳实践*或*建议*。

* **协议升级类GXIP**描述影响大多数或所有GXChain实施的变更，例如协议的更改，块或事务有效性规则的更改，或影响使用GXChain的应用程序的互操作性的任何更改及添加。

# 如何参与贡献

希望提交GXIP的人应首先在issue中提出他们的想法。讨论结束后，将获得一个gxip的编号，以这个编号为目录名提交状态为*draft*(草稿)Pull Request。一旦达成讨论参与者之间的共识，状态将变更为*Accept*(接受)。自此，不允许对文件进行重大更改。

如果提案需要协议升级，则只有在社区参与者批准了相应的工作人员或硬分叉提案时，才会考虑*实施*。信息类GXIP只能达到*接受*状态后才考虑实施，因为这类提案我们不强制执行它们

我们在这里列出GXIP草案完全自主的，因为其实际实施的最终决定是由GXChain社区参与者通过批准投票完成的。

强烈建议单个GXIP包含单个关键提议或新想法。小的增强或补丁通常不需要GXIP，可以通过向GXChain问题跟踪器提交补丁，将其注入GXChain开发工作流程。 GXIP越集中，它就越成功。 如果GXIP看起来太过分散或太宽泛，编辑人员保留拒绝GXIP提案的权利。如果有疑问，请将您的GXIP分成几个注重焦点的GXIP。

在编写GXIP之前公开征求一个想法是为了节省潜在的修改时间。此前有许多改变GXChain的想法，都因为各种原因被拒绝了。所以，请首先询问GXChain社区你的想法是否是原创的，这有助于防止花费太多时间在讨论在此前已经被拒绝的事情上（搜索互联网并不总是那么有效）。它还有助于确保该想法适用于整个社区而不仅仅是作者。一个想法对作者来说听起来不错并不意味着它适用于大多数使用GXChain的大多数人。

在讨论之后，该提案应该通过GXIP草案形式发送给GXChain开发人员和GXIP编辑人员。该草案必须以如下所述GXIP格式编写，否则将会被打回。

在GXIP编辑人员批准之后，他将为GXIP分配一个编号，标记它的状态为“draft”(草稿)，并将其添加到git仓库。 GXIP编辑人员不会无理拒绝GXIP。拒绝GXIP状态的原因包括重复工作，技术上不健全，没有提供适当的动机或解决向后兼容性，或者不符合GXChain理念。

GXIP作者可以根据需要在git仓库中更新草案。作者也可以通过提交Pull Request的方式对草案进行更新。

被接受的GXIP，它必须符合某些最低标准。它必须包含对提议改善的清晰和完整的描述。这些改动必须是净改善。如果适用，拟议的实施必须是可靠的，不得使协议复杂化。

GXIP发布后，必须完成参考实施部分。当参考实施完成并由股东通过批准投票接受时，状态将更改为“已接受”。 GXIP也可能被社区“拒绝”。

此外，GXIP可以被指定为“延期”状态。当GXIP没有取得进展时，GXIP作者或编辑人员可以为GXIP分配此状态。延迟GXIP后，GXIP编辑者可以将其重置为草稿状态。

GXIP也可以被不同的GXIP取代，使原始的过时。这适用于信息类GXIP，比如API的第2版可以替换版本1。

# GXIP包含哪些内容

每个GXIP *必须* 包含以下几个部分:

* Preamble -- RFC 822 style headers containing meta-data about the GXIP,
  including the GXIP number, a short descriptive title (limited to a maximum of
  44 characters), the names, and optionally the contact info for each author,
  etc.

* Abstract -- a short (~200 word) description of the technical issue being
  addressed.

* Copyright/public domain -- Each GXIP must either be explicitly labelled as
  placed in the public domain (see this GXIP as an example) or licensed under
  the Open Publication License.

* Motivation -- The motivation is critical for GXIPs that want to change the
  GXChain protocol. It should clearly explain why the existing protocol
  specification is inadequate to address the problem that the GXIP solves. GXIP
  submissions without sufficient motivation may be rejected outright.

* Rationale -- The rationale fleshes out the specification by describing what
  motivated the design and why particular design decisions were made. It should
  describe alternate designs that were considered and related work, e.g. how the
  feature is supported in other languages. The rationale should provide evidence
  of consensus within the community and discuss important objections or concerns
  raised during discussion.

* Specification -- The technical specification should describe the syntax and
  semantics of any new feature. The specification should be detailed enough to
  allow competing, interoperable implementations for any of the current
  GXChain platforms.

* Discussion -- The GXIP shall include a discussion on positive and negative
  effects on the GXChain ecosystem shall it be accepted by shareholders. This
  section is supposed to be the most important section for shareholders to grasp
  the full impact of the GXIP and help shareholders to make a decision.

* Summary for Shareholders -- Most GXIPs will probably be of technical nature.
  However, many shareholders are not as technical as the author of a particular
  GXIP. This non-technical paragraph serves as a place which can be used to
  to interact with shareholders and help them form their opinion. It is not
  meant to be a marketing driven paragraph to convince shareholders to vote
  **for** or **against** a proposal, though.

# GXIP Formats and Templates

GXIPs should be written in markdown format. Image files should be
included in a subdirectory for that GXIP. A template including the header
preamble is provided in [this repository](GXIPs-Template.md).

# GXIP Editors

The current GXIP editors are:

 * Albert <zhuliting@gxb.io>
 * David Lan <lanhaoxiang@gxb.io>

The editors don't pass judgement on GXIPs. We merely do the administrative &
editorial part.

Many GXIPs are written and maintained by developers with write access to the
GXChain codebase. The GXIP editors monitor GXIP changes, and correct any
structure, grammar, spelling, or markup mistakes we see.

For each new GXIP that comes in an editor does the following:

* Read the GXIP to check if it is ready: sound and complete. The ideas must make
  technical sense, even if they don't seem likely to be accepted.
* The title should accurately describe the content.
* Edit the GXIP for language (spelling, grammar, sentence structure, etc.),
  markup (for reST GXIPs), code style (examples should match GXIP 8 & 7).

Once the GXIP is ready for the repository it should be submitted as a "pull
request" to the [gxchain/gxips](https://github.com/gxchain/gxips) repository
on GitHub where it may get further feedback.

The GXIP editor will:

* Assign a GXIP number (almost always just the next available number, but
  sometimes it's a special/joke number, like 666 or 3141) in the pull request
  comments.
* Merge the pull request when the author is ready (allowing some time for
  further peer review).
* List the GXIP in [README.md](https://github.com/gxchain/gxips/blob/master/README.md)
* Send email back to the GXIP author with next steps (post to GXChain mailing
  list).

# History

This document was derived heavily from Python's PEP-0001 and Bitcoin BIP-0001.
In many places text was simply copied and modified. Although the
PEP-0001/BIP-0001 text was written by Barry Warsaw, Jeremy Hylton, and David
Goodger, they are not responsible for its use in the GXChain Improvement
Process, and should not be bothered with technical questions specific to
GXChain or the GXIP process. Please direct all comments to the GXIP editors
or the GXChain development mailing list.
