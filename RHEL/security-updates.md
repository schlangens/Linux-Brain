## Security

#### Security Updates

### Objectives:

At the end of this episode, I will be able to:

1. Use dnf to selectively install security updates separately from feature updates.
2. Navigate the Red Hat customer portal for security updates and CVEs.
3. Leverage Red Hat Insights to manage updates across multiple systems.

### External Resources:

- [Red Hat Customer Portal](https://access.redhat.com/)
- [Channel: Security](https://www.redhat.com/en/blog/channel/security)
- [Red Hat Insights](https://cloud.redhat.com/insights/overview)

`sudo dnf update`

`sudo dnf check-update --security`

`sudo dnf updateinfo cves`

`sudo dnf updateinfo advisory <number>`

### Just apply security updates

`sudo dnf update --security`
