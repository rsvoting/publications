# Random-Sample Voting: Real World Crypto 2016 Trial Report

The [Random-Sample-Voting Project](http://www.rsvoting.org) (the "Project")
ran its second public trial of the Random-Sample Voting system at
[Real World Crypto (RWC) 2016](http://www.realworldcrypto.com/rwc2016),
which was held in Stanford, California, in January 2016. The election employed
the complete protocol including all 250 audit tables. Attendees were asked
informally whether they would like to receive a ballot and vote. The trial
was a success and has helped guide future development.

## Objectives of the Real World Crypto 2016 Trial
The purpose of the RWC 2016 trial was, in addition to testing the technical
system, to obtain the reaction of the attendees. It was hoped that those who
voted would provide feedback not only on security of the system but on its
usability as well.

## Details of the Real World Crypto 2016 Trial
We proposed the following question for the RWC 2016 trial:
> *"Have any popular Diffie-Hellman-1024 primes been broken?"*

The election configured was based on an estimation of the conference
attendance, with 450 real ballots and 50 decoy ballots. To ensure with near
certainty that no ballots would be duplicated, the election was defined to have
a roster size of 1,000,000. The poll ran during the conference, from midnight
on Wednesday January 6 through 9am on Friday January 8. Our field team
distributed paper ballots to conference attendees until the close of polls. An
unvoted sample ballot is available
[here](http://rsvoting.org/trials/201601-rwc/rwc-2016-ballot-299.pdf).

### Election Software
The software deployed for the trial was an improved version of the full system
used at Crypto 2015, including the election authority software, the audit
bulletin board (ABB), voter bulletin board (VBB), and verifiable random beacon.

In the interest of transparency, the software used in the trial is available
upon request for auditing and research purposes. Please direct all requests to
[software (at) rsvoting.org](mailto:software [at] rsvoting.org). The software that may
be requested include:

* Election Authority
* Audit Bulletin Board
* Voter Bulletin Board

### Verifiable Random Bit Generation
Two different entropy sources were, for the first time, used in a single
election: the New York Stock Exchange for the random selection and the NIST
random beacon for the audit.

#### Stock Market Random Bit Generation
The bits used for the initial draw were derived from data retrieved from the
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

#### NIST Random Beacon Bits
The bits used for the final draw were acquired from the NIST random beacon.
The United States
[National Institute of Standards](http://www.nist.gov/itl/csd/ct/nist_beacon.cfm)
publishes "random" values every minute online via their
[random beacon](https://beacon.nist.gov/). They are not as "un-manipulatable"
as the stock market data, but can be helpful when bits are needed at times
other than market closing. (In future, it is hoped that the RSV protocol's
division into batches can be done based on more than one source of randomness,
one allowing immediate posting of results and the other providing more integrity
later.)

## Election Procedure
Random-sample elections have many steps whose execution must not overlap. The
timeline below describes the events that took place to successfully run the
trial. The Project managed the election through the Election Authority
software.

* Monday, January 4, 2016, 17:04 UTC - The Project published the election
  definition and commitments to the ABB and VBB.
* Monday, January 4, 2016, 20:15 UTC - The New York Stock Exchange closed and
  the verifiable randomness for the Initial Draw was determined.
* Tuesday, January 5, 2016, 00:30 UTC - The New York Stock Exchange published
  the daily summary through the Consolidated Tape Association. The random
  beacon committed to in the election definition derived the bits for the
  initial draw.
* Tuesday, January 5, 2016, 15:16 UTC - The Project queried the random beacon
  for the initial draw's verifiable random bits. The Project published the
  initial draw to the ABB, committed the final summands to the ABB, and
  published the ballot authentication information to the VBB.
* Wednesday, January 6, 2016 - The Project's field team printed the ballots.
* Wednesday, January 6, 2016, 00:00 UTC - The VBB opened the polls and began
  accepting votes. The field team began distributing ballots, which included
  instructions for voting.
* Friday, January 8, 2016, 18:00 UTC - The VBB closed the polls and stopped
  accepting votes.
* Friday, January 8, 2016, 18:12 UTC - The Project downloaded the votes from
  the VBB, generated the print audit and tally information, and committed the
  data to the ABB in preparation for the final draw.
* Friday, January 8, 2016, 18:30 UTC - The NIST random beacon began generating
  randomness to be used for the Final Draw.
* Friday, January 8, 2016, 19:00 UTC - The NIST random beacon finished
  generating the random bits for the Final Draw query and the verifiable
  randomness for the Final Draw was determined.
* Friday, January 8, 2016, 19:09 UTC - The Project queried the random beacon
  for the final draw's verifiable random bits.
*  Friday, January 8, 2016, 19:54 UTC - The Project revealed the first two
  batches of auditable columns on the ABB based on the final draw.
* Friday, January 8, 2016, 19:59 UTC - The Project revealed the second two
  batches of auditable columns on the ABB based on the final draw.
* Friday, January 8, 2016, 20:06 UTC - The Project revealed the final batch of
  auditable columns on the ABB based on the final draw.
* Friday, January 20, 2016 (midday PST) - The Project announced the results of
  the election.

## Election Results and Audit
A total of 21 ballots were voted, of which 20 were real and 1 was a  decoy. Of
the 20 real ballots, 17 believed at least one popular Diffie-Hellman prime has
been broken, whereas 3 disagreed.

No duplicate ballots were generated from this configuration. The roster size was
chosen to be large enough to ensure almost certainly that no duplicate ballots
would be generated.

A cursory audit of the election was conducted by the Project, which entailed
manual inspection that the data published to the ABB was consistent. An
independent audit of the election has not yet been performed, as far as the
Project is aware. The fully auditable election data derived from the VBB and
ABB is available, allowing anyone to conduct a more complete, independent
audit.

* [Election Authority certificate](http://rsvoting.org/trials/201601-rwc/EA.pem)
* [VBB data](http://rsvoting.org/trials/201601-rwc/rwc-2016-demo-VBB.zip)
* [ABB data](http://rsvoting.org/trials/201601-rwc/rwc-2016-demo-ABB.zip)

## Caveats
This trial did not employ all of the procedural controls one would expect of
a real election. In a real election, for full privacy protection, we would
handle ballot printing and distribution with appropriate controls to protect
the secrecy of the vote codes and the privacy of the voter.

## Lessons Learned
This trial operated on a compressed schedule to allow time for announcing the
results during Real World Crypto. This introduced additional administrative
challenges over the Crypto 2015 trial.

1.  For the final draw, we used the NIST random beacon, which some may perceive
    as less than ideal with respect to verifiability. Having multiple audits
    using increasingly higher quality bits enables fast results with
    high-assurance.
1.  It was discovered that full auditability is not possible unless external
    parties can verify the commitments to the election definition and
    configuration were made prior to the initial draw. Two options have been
    proposed for addressing this:
    1.  Use a subscriber list to announce when election definitions and
        commitments are published.
    1.  Use a variant of the protocol that incorporates external timestamping
        to prove the commitments were published prior to the initial draw.
1.  System redundancy and availability was one of the lessons learned from the
    Crypto 2015 trial. Though we did not enact a redundant system for this
    trial, we developed a contingency plan to amend the election definition if
    system failures occurred. System redundancy remains a high priority item
    for the Project.

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

## Appendix: NIST Random Beacon
At the time of publication, the [NIST random beacon](https://beacon.nist.gov/)
uses two independent hardware true random number generators (TRNG) made with
SP 800-90 compliant components. Together, these TRNGs generate 512 bits each
minute. Each record is chained, timestamped, and signed by NIST.

