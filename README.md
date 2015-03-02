# Phriak
Phriak is a Smalltalk client for the [Riak NoSQL database](http://basho.com/riak/) (primarily for [Pharo Smalltalk](http://pharo.org/)).

This is a GitHub mirror of [Phriak's SmalltalkHub Monticello repository](http://smalltalkhub.com/#!/~gokr/Phriak) (using [FileTree](https://github.com/dalehenrich/filetree)).

Phriak started as a friendly fork from Runar Jordahl's original [EpigentRiakInterface](http://blog.epigent.com/2011/03/riak-interface-for-pharo-smalltalk.html). Riak is a screamingly cool NoSQL database that scales like crazy. This Riak interface implementation uses Zinc HTTP and the JSON package.

## Installing the Package
The easiest way to load it into a Pharo 2.0+ image is via Metacello.

Add a SmalltalkHub Monticello repository:

```smalltalk
MCSmalltalkhubRepository
	owner: 'gokr'
	project: 'Phriak'
	user: ''
	password: ''
```

Install the ```ConfigurationOfPhriak``` package. Then ```load``` the dependencies:

```smalltalk
(ConfigurationOfPhriak project version: '0.7') load
```

## Running the Tests
### Unit Tests
The subclasses of ```RiakTestCase``` (such as ```RiakObjectTests```) are intended to be 
unit tests, and don't need a running Riak instance. Those should all pass as-is.

### Integration Tests
The subclasses of ```PhriakIntegrationTestCase``` require an instance of Riak to connect to.

1. Install Riak. On Mac OS X, use [brew install](http://docs.basho.com/riak/latest/ops/building/installing/mac-osx/#Homebrew) or use the pre-built installer at [Riak204.dmg](http://basho.s3.amazonaws.com/Riak204.dmg). On Ubuntu Linux, I recommend [installing from apt or from .deb](http://docs.basho.com/riak/latest/ops/building/installing/debian-ubuntu/))
2. Start riak (usually just ```riak start```), take note of which HTTP port it's listening on (```8098``` by default).
3. Point your test client to the right hostname and port. In ```PhriakIntegrationTestCase>>#clientForTesting```, edit the host and port variables if using non-defaults.

    ```smalltalk
    clientForTesting	"Return an instance of a Riak HTTP client pointing to a test cluster"		^RiakClient http		host: 'localhost';		port: 8098;		yourself.	```