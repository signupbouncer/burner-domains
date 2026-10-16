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

## Check signups against this list

To check each signup from your server, call our API before you create the user. On the Free plan, you can sign up
without a card. Get a key at https://signupbouncer.com/signup and keep it in an environment variable.

```sh
curl https://signupbouncer.com/v1/check \
  -H "Authorization: Bearer $SIGNUPBOUNCER_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"email": "someone@mailinator.com"}'
```

Refuse the signup when `action` is `"block"`. If the call fails or takes longer than 1.5 seconds, let the signup
through. New apps start in shadow mode, where `action` is always `"allow"`, until you switch the app to enforce on your
dashboard.

Besides this list, we look up each domain's mail servers and count repeat signups from one Gmail inbox. Code for
Next.js, Express, Python, Firebase and more is at https://signupbouncer.com/docs#code.

To check one address from an AI assistant, add the MCP server `https://signupbouncer.com/mcp`. It needs no key.

To see how many of your existing users signed up with throwaway addresses, run the free audit at
https://signupbouncer.com/audit. The audit sends us only email domains and counts.

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
