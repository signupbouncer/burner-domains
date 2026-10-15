# Disposable email domains

A list of disposable (temporary, throwaway) email domains, one per line, in `burner-domains.txt`. It is the public part
of the data behind [signupbouncer](https://signupbouncer.com), which checks signups for throwaway addresses.

## How the list is made

- It merges three open lists:
  [disposable-email-domains](https://github.com/disposable-email-domains/disposable-email-domains),
  [ivolo/disposable-email-domains](https://github.com/ivolo/disposable-email-domains) and
  [7c/fakefilter](https://github.com/7c/fakefilter).
- It adds domains offered by temp-mail websites. A scraped domain is added only when its mail server is a known
  disposable-mail server, never on the website's word alone.
- It removes every domain on a curated allowlist of real mailbox providers, entries that are public suffixes (such as
  `co.uk`), and government, education and military domains unless their mail goes to a known disposable-mail server.

## How it is updated

- A domain appears here once it has been on signupbouncer's list for 24 hours without a break.
- A domain signupbouncer stops listing is removed here within about two hours.
- New domains are pushed once a day; removals are pushed on the next hourly run.

Lines starting with `#` are comments: what the file is, the data version, and the upstream licence notices.

## Using it

Download `burner-domains.txt` from this repository's raw URL and match an address's domain and its parent domains
against it (a listed `example.com` also covers `mail.example.com`). Ignore lines starting with `#`.

A domain listed by mistake? Open an issue with the domain and why it is a real mailbox provider.

## Licence

signupbouncer's own contribution to this list (the domains it finds itself, and how the list is put together) is
dedicated to the public domain under CC0 1.0 (`LICENSE`): use it for anything, no attribution needed. The list also
contains data from these lists, which stays under their own licences:

- disposable-email-domains: CC0 1.0 (`LICENSE.disposable-email-domains`);
- ivolo/disposable-email-domains: MIT (`LICENSE.ivolo`, the licence section of that project's README);
- 7c/fakefilter: BSD 3-Clause (`LICENSE.fakefilter`).

If you redistribute the whole list, keep those notices with it.

Their notices are also repeated at the top of `burner-domains.txt`. The authors of those lists do not endorse this list
or signupbouncer.
