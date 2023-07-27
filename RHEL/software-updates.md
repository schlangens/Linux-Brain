## Introduction to RHEL

#### Software Updates

### Objectives:

At the end of this episode, I will be able to:

1. Determine if there are pending updates for a system.
2. Perform system updates and automate the process if desired.

## Server GUI

`super key + search for subscription`

## Command line registration

`sudo subscription-manager list`
`sudo subscription-manager register --username=<username for rhel> --password=<password>`

`sudo subscription-manager attach --auto`
`sudo subscription-manager list --available`
`sudo subscrition-manager list --consumed`

## Updating your system

`sudo dnf lists`
`sudo dnf update -y`

### Yum works as well as DNF

`sudo yum install mc -y`
`sudo dnf install mc -y`
`sudo dnf remove mc -y`

### Rollback that shit

`sudo dnf history`
`sudo dnf history undo 16`
