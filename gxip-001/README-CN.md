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

# GXIP类型

GXIP分为两种：

* **信息类GXIP**描述GXChain设计问题，或向GXChain社区提供一般指南或信息，但不提议新功能，协议更改或任何其他修改。信息类GXIP不一定代表GXChain社区的共识或建议，因此用户和实施者可以自行选择是忽略信息类GXIP还是遵循他们的建议。比如*最佳实践*或*建议*。

* **协议升级类GXIP**描述影响大多数或所有GXChain实施的变更，例如协议的更改，块或事务有效性规则的更改，或影响使用GXChain的应用程序的互操作性的任何更改及添加。

# 参与贡献

希望提交GXIP的人应首先在issue中提出他们的想法。讨论结束后，将获得一个gxip的编号，以这个编号为目录名提交状态为*draft*(草稿)Pull Request。一旦达成讨论参与者之间的共识，状态将变更为*Accept*(接受)。自此，不允许对文件进行重大更改。

如果提案需要协议升级，则只有在社区参与者批准了相应的工作人员或硬分叉提案时，才会考虑*实施*。信息类GXIP只能达到*接受*状态后才考虑实施，因为这类提案我们不强制执行它们

我们在这里列出GXIP草案完全自主的，因为其实际实施的最终决定是由GXChain社区参与者通过批准投票完成的。

强烈建议单个GXIP包含单个关键提议或新想法。小的增强或补丁通常不需要GXIP，可以通过向GXChain问题跟踪器提交补丁，将其注入GXChain开发工作流程。 GXIP越集中，它就越成功。 如果GXIP看起来太过分散或太宽泛，编辑人员保留拒绝GXIP提案的权利。如果有疑问，请将您的GXIP分成几个注重焦点的GXIP。

在编写GXIP之前公开征求一个想法是为了节省潜在的修改时间。此前有许多改变GXChain的想法，都因为各种原因被拒绝了。所以，请首先询问GXChain社区你的想法是否是原创的，这有助于防止花费太多时间在讨论在此前已经被拒绝的事情上（搜索互联网并不总是那么有效）。它还有助于确保该想法适用于整个社区而不仅仅是作者。一个想法对作者来说听起来不错并不意味着它适用于大多数使用GXChain的大多数人。


在讨论之后，该提案应该通过GXIP草案发送给GXChain开发人员和GXIP编辑人员。该草案必须以如下所述GXIP格式编写，否则可能会被打回。

If the GXIP editor approves, he will assign the GXIP a number, label it, give it
status "Draft", and add it to the git repository. The GXIP editor will not
unreasonably deny a GXIP. Reasons for denying GXIP status include duplication
of effort, being technically unsound, not providing proper motivation or
addressing backwards compatibility, or not in keeping with the GXChain
philosophy.

The GXIP author may update the Draft as necessary in the git repository. Updates
to drafts may also be submitted by the author as pull requests.

For a GXIP to be accepted it must meet certain minimum criteria. It must be a
clear and complete description of the proposed enhancement. The enhancement must
represent a net improvement. The proposed implementation, if applicable, must be
solid and must not complicate the protocol unduly.

Once a GXIP has been published, the reference implementation must be
completed.  When the reference implementation is complete and accepted
by the shareholders via approval voting, the status will be changed to
"Accepted". A GXIP can also be "Rejected" by shareholders.

Furthermore, a GXIP can be assigned status "Deferred". The GXIP author or editor
can assign the GXIP this status when no progress is being made on the GXIP. Once
a GXIP is deferred, the GXIP editor can re-assign it to draft status.

GXIPs can also be superseded by a different GXIP, rendering the original
obsolete. This is intended for Informational GXIPs, where version 2 of an API
can replace version 1.

# What belongs in a GXIP?

Each GXIP *should* have the following parts:

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
