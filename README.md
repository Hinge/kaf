# Kaf

## Install
Run `go install` from `cmd/kaf` directory

The Hinge fork has additional features for working with Confluent Schema Header messages. It supports consuming and producing with Confluent Schema Headers.

## Usage
See below/command help for general usage instructions. This section focuses on use cases involving functionality that has been added in the fork.

### Consume from topic with Confluent Headers
```
kaf --cluster prod-ue1-confluent-01 consume onboarding-complete-v1 --proto-include /path/to/shared-protobuf/kafka/ --proto-type onboarding.OnboardingComplete --confluent-header
```

### Query for message with key in topic with Confluent Headers
```
kaf --cluster prod-ue1-confluent-01 query prod-shield-user-eligible-v1 --key $querykey --proto-include /path/to/shared-protobuf/kafka/ --proto-type shield.UserEligible --confluent-header
```

### Produce message to topic with Confluent Headers
```
kaf --cluster prod-ue1-confluent-01 produce prod-shield-user-eligible-v1 --key $msgkey --schema-registry-key $schemakey --schema-registry-secret $schemasecret --schema-registry-url $schemaurl
```

## Original Readme
Kafka CLI inspired by kubectl & docker

[![Actions Status](https://github.com/birdayz/kaf/workflows/Go/badge.svg)](https://github.com/birdayz/kaf/actions)
[![GoReportCard](https://goreportcard.com/badge/github.com/birdayz/kaf)](https://goreportcard.com/report/github.com/birdayz/kaf)
[![GoDoc](https://godoc.org/github.com/birdayz/kaf?status.svg)](https://godoc.org/github.com/birdayz/kaf)
![AUR version](https://img.shields.io/aur/version/kaf-bin)

![asciicinema](asciicinema.gif)

## Install
Install via Go from source:

```
go install github.com/birdayz/kaf/cmd/kaf@latest
```

Install via install script:

```
curl https://raw.githubusercontent.com/birdayz/kaf/master/godownloader.sh | BINDIR=$HOME/bin bash
```

Install on Archlinux via [AUR](https://aur.archlinux.org/packages/kaf-bin/):

```
yay -S kaf-bin
```

Install via Homebrew:

```
brew tap birdayz/kaf
brew install kaf
```

## Usage

Show the tool version

`kaf --version`

Add a local Kafka with no auth

`kaf config add-cluster local -b localhost:9092`

Select cluster from dropdown list

`kaf config select-cluster`

Describe and List nodes

`kaf node ls`

List topics, partitions and replicas

`kaf topics`

Describe a given topic called _mqtt.messages.incoming_

`kaf topic describe mqtt.messages.incoming`

List consumer groups

`kaf groups`

Describe a given consumer group called _dispatcher_

`kaf group describe dispatcher`

Write message into given topic from stdin

`echo test | kaf produce mqtt.messages.incoming`

Set offset for consumer group _dispatcher_ consuming from topic _mqtt.messages.incoming_ to latest for all partitions

`kaf group commit dispatcher -t mqtt.messages.incoming --offset latest --all-partitions`

## Configuration
See the [examples](examples) folder

## Shell autocompletion
Source the completion script in your shell commands file:

Bash Linux:

```kaf completion bash > /etc/bash_completion.d/kaf```

Bash MacOS:

```kaf completion bash > /usr/local/etc/bash_completion.d/kaf```

Zsh

```kaf completion zsh > "${fpath[1]}/_kaf"```

Fish

```kaf completion fish > ~/.config/fish/completions/kaf.fish```

Powershell

```Invoke-Expression (@(kaf completion powershell) -replace " ''\)$"," ' ')" -join "`n")```

## Sponsors
### [Redpanda](https://github.com/redpanda-data/redpanda)
- The streaming data platform for developers
- Single binary w/no dependencies
- Fully Kafka API compatible
- 10x lower P99 latencies, 6x faster transactions
- Zero data loss by default
