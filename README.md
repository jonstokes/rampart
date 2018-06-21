# rampart

One problem with some popular DLTs is lack of write bandwidth; reads are cheap and infinitely scalable, but writes directly to the blockchain are bottlenecked by a number of fundamental technical limitations.

What if there was a way to turn this bug into a feature, though?

Imagine the inverse of the [bitcoin scalability problem](https://en.wikipedia.org/wiki/Bitcoin_scalability_problem) -- writes are scalable, but reads are greatly bandwidth constrained. A database that's easy to write to but very difficult and expensive to read from sounds like a terrible technology, but it's an excellent fit for one peculiar problem: a **centralized firearm registry**, where each record stores a chain of custody for a single firearm and is indexed by serial number (probably combined with some other metadata, like make and model).

Think about it. The primary rationale that gun control advocates offer for a gun registry is ease of tracing crime guns. But gun rights advocates are worried that a centralized registry of guns will inevitably lead to confiscation.

A a gun registry that can only be read from a few hundred times per day would address both of these concerns. Law enforcement would have the ability to trace a few hundred crime guns per day, but at such a low read rate there would be no way to compile a big enough unencrypted list of the nation's hundreds of millions of guns or tens of millions of gun owners.

## Possible implementations

A fairly simple and naive implementation of such a database would be one in which a record of a firearm transaction between two parties is created and encrypted locally, and the keys are discarded before the encrypted transaction is sent off for storage in a central database. Because the keys have been thrown away, anyone wanting to read the record would have to throw compute power at the problem of decrypting it, and this would make writes expensive and slow.

Depending on the encryption algorithm selected and the key size, we could tune the difficulty of cracking the records so as to keep the practical read bandwidth below some desired threshold.

This scheme has a number of problems, though, the main one being that if the encryption algorithm we selecte ever falls to some computationally cheap attack, then the entire database is compromised.

Another possible implementation might be to require a block to be written to a public, write-constrained blockchain like bitcoin before a read can be carried out in the database. I'm still thinking about how this might work, though.

## A rhetorical intervention disguised as a technological invention

Gun controllers will complain that this database doesn't enable law enforcement to look up all the guns held by a specific owner; they'll claim they need this ability so they can take weapons from people who are deemed unfit by virtue of a mental illness diagnosis, suicide attempt, domestic violence conviction, etc.

This complaint is correct; this database does not support any sort of confiscatory use case _by design_. Rather, the point of the database is to neutralize the primary "tough on crime" rationale that gun controllers give for wanting a central gun registry, and to take that off the table entirely, leaving them with "confiscation" as their only argument for a standard gun registry. 

Note that this database doesn't actually have to exist as anything other than a proposal and a working codebase for gun rights advocates to get most of the benefit of it. If all it succeeds in doing is to take tracing crime guns off the table as the stated rational for a registry, then it will be a success.

**Note**: Some will be offended at the apparent lack of good faith in this proposal, but I take it as a given that gun registries [are dumb and don't work](https://www.forbes.com/sites/danielfisher/2013/01/22/canada-tried-registering-long-guns-and-gave-up/#39511a495a1b). A read-constrained database like the one proposed here might be an acceptable way to prove that point here in the US, while keeping confiscation off the table.