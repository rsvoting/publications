# Random-Sample Voting: CRYPTO 2015 Trial Report

The [Random-Sample-Voting Project](http://www.rsvoting.org) (the "Project")
ran its first public trial of the Random-Sample Voting system at
[Crypto 2015](https://www.iacr.org/conferences/crypto2015/), the 35th
conference of the International Association for Cryptologic Research, which
was held in Santa Barbara, California, in mid-August. The election employed
the complete protocol including all 250 audit tables. Attendees were asked
informally whether they would like to receive a ballot and vote. The trial
was a success and has helped guide future development.

## Objectives of the Crypto 2015 Trial
The purpose of the Crypto 2015 trial was, in addition to testing the technical
system, to obtain the reaction of the attendees at the event. It was hoped that
those who voted would provide feedback not only on the overall system but on its
usability as well.

The trial was a follow-up to talks given at Rump Sessions at Crypto 2013 and
2014.

## Details of the Crypto 2015 Trial
We proposed the following question for the Crypto 2015 trial:
> *"Do you believe 2048-bit RSA key will be secure against brute-force attacks
> in 2020?"*

The election configured was based on an estimation of the conference
attendance. The election was configured for a roster size of 1,000, with 150
real ballots and 150 decoy ballots. The poll ran from midnight on Sunday,
August 16, through noon on Wednesday, August 19, during the conference. Our
field team distributed paper ballots to conference attendees until the close of
polls. An unvoted sample ballot is available
[here](http://rsvoting.org/trials/201508-crypto/crypto-2015-ballot-299.pdf).

### Election Software
The software deployed for the trial was an alpha version of the full system,
including the election authority software, the audit bulletin board (ABB), voter
bulletin board (VBB), and verifiable random beacon.

In the interest of transparency, the software used in the trial is available
upon request for auditing and research purposes. Please direct all requests to
[software (at) rsvoting.org](mailto:software [at] rsvoting.org). The software that may
be requested include:

* Election Authority
* Audit Bulletin Board
* Voter Bulletin Board

### Stock Market Random Bit Generation
The bits used for the trial were derived from data retrieved from the
[Consolidated Tape Association](https://www.ctaplan.com/) (CTA), the reporting
authority for the [New York Stock Exchange](https://www.nyse.com/). The
extraction algorithm used was a Blowfish-256
[CBC-MAC extractor](https://www.iacr.org/archive/crypto2004/31520493/clean.pdf).
Only stocks with modest volume were used (at least 10,000 trades). A detailed
description of the extractor is described in the Appendix.

Due to the precision reported by the CTA, prices from unofficial reporting
outlets may not yield the same bits as those derived from the CTA’s reporting.
In the event of a dispute, the CTA's reporting is considered correct as the
reporting authority.

## Election Procedure
Random-sample elections have many steps whose execution must not overlap. The
timeline below describes the events that took place to successfully run the
trial. The Project managed the election through the Election Authority
software.

* Friday, August 14, 2015, 16:44 UTC - The Project published the election
  definition and commitments to the ABB and VBB.
* Friday, August 14, 2015, 20:15 UTC - The New York Stock Exchange closed and
  the verifiable randomness for the Initial Draw was determined.
* Saturday, August 15, 2015, 00:30 UTC - The New York Stock Exchange published
  the daily summary through the Consolidated Tape Association.  The random
  beacon committed to in the election definition derived the bits for the
  initial draw.
* Saturday, August 15, 2015, 18:19 UTC - The Project queried the random beacon
  for the initial draw's verifiable random bits. The Project published the
  initial draw to the ABB, committed the final summands to the ABB, and
  published the ballot authentication information to the VBB.
* Saturday, August 15, 2015 (evening) - The Project's field team printed the
  ballots.
* Sunday, August 16, 2015, 7:00 UTC - The VBB opened the polls and began
  accepting votes. The field team began distributing ballots, which included
  instructions for voting.
* Wednesday, August 19, 2015, 19:00 UTC - The VBB closed the polls and stopped
  accepting votes.
* Wednesday, August 19, 2015, 19:09 UTC - The Project downloaded the votes from
  the VBB, generated the print audit and tally information, and committed the
  data to the ABB in preparation for the final draw.
* Wednesday, August 19, 2015, 20:15 UTC - The New York Stock Exchange closed
  and the verifiable randomness for the Final Draw was determined.
* Thursday, August 20, 2015, 4:05 UTC - The Project queried the random beacon
  for the final draw's verifiable random bits. The Project revealed the
  auditable columns on the ABB based on the final draw.
* Thursday, August 20, 2015 (morning) - The Project announced the results of
  the election.

## Election Results and Audit
A total of 33 ballots were voted, of which 28 were real and 5 were decoys. Of
the 28 real ballots, 16 believed 2048-bit RSA would be secure against
brute-force attacks in 2020, whereas 12 disagreed.

Duplicate ballots were handled per the version of the protocol published at the
time of the election:

> If the initial draw assigns multiple real ballots to the same voter on the
> roster, all of that voter’s real ballots are cancelled as duplicates. The
> cancelled ballots are never printed.

Of the 300 ballot candidates generated randomly, 50 were duplicates and excluded
or "cancelled" by the protocol. In a more typical election, where the number of
ballots is small compared to the roster size, the number of cancellations should
with high probability be nearly zero. The unusually high number of cancellations
was a side-effect in how the Project chose to define the election, which had a
high quantity of ballots compared to the roster size.

A cursory audit of the election was conducted by the Project, which entailed
manual inspection that the data published to the ABB was consistent. An
independent audit of the election has not yet been performed, as far as the
Project is aware. The fully auditable election data derived from the VBB and
ABB is available, allowing anyone to conduct a more complete, independent
audit.

* [Election Authority certificate](http://rsvoting.org/trials/201508-crypto/EA.pem)
* [VBB data](http://rsvoting.org/trials/201508-crypto/crypto-2015-demo-VBB.zip)
* [ABB data](http://rsvoting.org/trials/201508-crypto/crypto-2015-demo-ABB.zip)

## Caveats
This trial did not employ all of the procedural controls one would expect of
a real election. In a real election, for full privacy protection, we would
handle ballot printing and distribution with appropriate controls to protect
the secrecy of the vote codes and the privacy of the voter.

## Lessons Learned
Based on informal observation of the voters—all of whom were from the rather
special population used in the test—receiving ballots, the following informal
observations were made:

1.  Voters seemed to have no questions about how to use the ballot to vote.
1.  When looking at the ballot for the first time, the fact that the two halves
    related to the same contest and a single vote was not immediately obvious
    to voters. Designing a simple, intuitive, and usable ballot for this system
    remains an open area of research.
1.  When handed a ballot, voters seemed curious about the overall context of
    the election. It seemed that a written explication of the significance,
    context, and nature of the test would have been appreciated by voters.

We did not test the indistinguishability of decoy ballots; however, the
possibility was raised for such a setting, where everyone at the event is able
to vote, of creating a challenge to allow participants to try to distinguish
decoys.

As election administrators, we achieved our goal of running a smooth election.
The bulletin boards remained available throughout the course of the elections
and voters did not comment on the technical aspects of the election. From the
administrative perspective, we made several observations:

1.  **Software Robustness:** By accident, we attempted to perform the final
    draw ahead of schedule. Fortunately, the election authority software was
    robust enough to catch this and inform us it was not yet time. However, the
    user interface should be robust enough to prevent the election authority
    from even attempting to make mistakes like these in the first place.
1.  **Standard Operating Procedures:** As our first public trial, we did not
    have documented procedures to follow beyond those enforced by the election
    authority software. The accident mentioned previously could have been
    prevented by following a documented procedure in addition to trusting the
    software’s protocol enforcement logic.
1.  **Trustee-based Authority:** We used a single individual for running the
    election authority software. In addition to protecting against attempts of
    malfeasance, a trustee system could help prevent accidental procedural
    errors and software user errors; and offer additional reasons for users to
    trust the administration of the election.
1.  **System Redundancy:** During the election, there were concerns regarding
    the scenario of system failure to include the election authority data, the
    bulletin boards, and the random beacon. Specifically, the beacon required
    software updates to its data harvesters shortly before the election. At
    some point, we need to address how to incorporate redundancy into the
    different softwares.

## Plans for the Next Trial
The Project intends to conduct the next trial at Real World Crypto 2016 in
January.

## Appendix: Random Beacon's Stock Market Extractor
The extraction algorithm used was a Blowfish-256
[CBC-MAC](https://www.iacr.org/archive/crypto2004/31520493/clean.pdf)
extractor.  Only stocks with modest volume were used (at least 10,000 trades).

The extractor was configured with the following key and IV:
* Key: 0x277a40d043858cd6b3b75cdccac084b2963846bdd91fb2f9243a27db0209e8d5
* IV: 0x0

The stocks were sorted lexicographically by exchange symbol and broken into
groups of 60 to generate a conservative 128-bits per group. Each group was
formatted as follows (all ASCII):

> `YYYY-MM-DD|Symbol-1|Price-1|Symbol-2|Price-2|...`

The buffer fed to the extractor was pre-pended with the length of the buffer
and padded using ISO/IEC 9797-1 (i.e., a 1 bit followed by 0s).  All values
fed through the extractor were in Big Endian.

