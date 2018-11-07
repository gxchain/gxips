    GXIP: 0001
    Title: GXIP Purpose and Guidelines
    Authors: Albert <zhuliting@gxb.io>
    Status: Draft
    Type: Informational
    Created: 2018-11-07

# What is a GXIP?

GXIP stands for GXChain Improvement Proposal but can also seen as an
improvement *protocol*. A GXIP is a design document providing information to the
GXChain community, or describing a new feature for GXChain or its processes
or environment. The GXIP should provide a concise technical specification of the
feature or the idea and a rationale for it. It may not only describe technical
improvements but also document *best-practises* and recommendations.

We intend GXIPs to be the primary mechanisms for proposing new features, for
collecting community input on an issue, and for documenting the design decisions
that have gone into GXChain. The GXIP author is responsible for building
consensus within the community and documenting dissenting opinions.

Because the GXIPs are maintained as text files in a versioned repository, their
revision history is the historical record of the feature proposal.

# GXIP Types

There are two kinds of GXIPs:

* An **Informational** GXIP describes a GXChain design issue, or provides general
  guidelines or information to the GXChain community, but does not propose a
  new feature, protocol change or any other modification. Informational GXIPs do
  not necessarily represent a GXChain community consensus or recommendation,
  so users and implementors are free to ignore Informational GXIPs or follow
  their advice. Examples would be *best-practises* or *recommendations*.
* A **Protocol** Upgrade GXIP describes any change that affects most or all
  GXChain implementations, such as a change to the protocol, a change in block
  or transaction validity rules, or any change or addition that affects the
  interoperability of applications using GXChain.

# Contributing

People wishing to submit GXIPs first should propose their idea as github
issue first. After discussion you will be assigned a number for the bsip
and can send a pull request for your *draft*. Once consensus among
discussion participants is reached, the status can be switched to
*accepted*. From this time on, major changes of the document will not be
permitted.

If the proposal requires a protocol upgrade, the proposal is considered
*implemented* only if shareholders have approved a corresponding worker or
hard fork proposal. Informational GXIPs can only reach the *accepted*
state since their implementation is not enforced by the blockchain.

We are fairly liberal with listing GXIP drafts here since the
final decision of its actual implementation is made solely by GXChain
shareholders via approval voting.

It is highly recommended that a single GXIP contain a single key
proposal or new idea. Small enhancements or patches often don't need a
GXIP and can be injected into the GXChain development work flow with a
patch submission to the GXChain issue tracker. The more focused the
GXIP, the more successful it tends to be. The GXIP editor reserves the
right to reject GXIP proposals if they appear too unfocused or too
broad. If in doubt, split your GXIP into several well-focused ones.

Vetting an idea publicly before going as far as writing a GXIP is meant to save
the potential author time. Many ideas have been brought forward for changing
GXChain that have been rejected for various reasons. Asking the GXChain
community first if an idea is original helps prevent too much time being spent
on something that is guaranteed to be rejected based on prior discussions
(searching the internet does not always do the trick). It also helps to make
sure the idea is applicable to the entire community and not just the author.
Just because an idea sounds good to the author does not mean it will work for
most people in most areas where GXChain is used.

Following a discussion, the proposal should be sent to the GXChain developers
and the GXIP editors with the draft GXIP. This draft must be written in GXIP
style as described below, else it will be sent back without further regard until
proper formatting rules are followed.

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
