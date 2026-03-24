# Legal and Authorisation

Revelion is a penetration testing tool. Like Nmap, Burp Suite, or Metasploit, it is the user's responsibility to ensure it is used lawfully. The platform provides no authorisation by itself — you must obtain explicit written permission before testing any system.

!!! warning "Unauthorised access to computer systems is a criminal offence. Always obtain explicit written permission before testing."
    In the UK, unauthorised access is an offence under the **Computer Misuse Act 1988**. In the EU and US, equivalent laws apply. Ignorance of authorisation requirements is not a defence.

## Your responsibilities

By using Revelion, you confirm that:

1. You own the systems being tested, or you hold **explicit written authorisation** from the owner
2. Your testing activity falls within the agreed scope of any authorisation you hold
3. You comply with all applicable laws in your jurisdiction and in the jurisdiction of the target systems
4. You do not use Revelion to test systems for which you do not have authorisation, regardless of whether those systems appear vulnerable

## Scope enforcement

Revelion includes built-in scope enforcement. Agents are instructed to operate only within the targets defined at scan creation. They are prohibited from following links, redirects, or discovered references that lead outside the defined scope.

This enforcement is a safeguard, not a substitute for proper authorisation. Scope enforcement operates at the agent instruction level — it reduces out-of-scope activity but does not guarantee it with absolute certainty in all edge cases.

## Acceptable use

Revelion may not be used for:

- Testing systems without authorisation
- Attacks against critical national infrastructure
- Any activity that constitutes a criminal offence under applicable law
- Harassment, stalking, or targeting individuals
- Circumventing access controls for purposes outside an authorised pentest scope

Violations of the acceptable use policy will result in immediate account termination and may be reported to relevant authorities.

## Limitation of liability

Revelion provides the platform and tooling. Users are solely responsible for how they use it. Revelion Limited accepts no liability for damages resulting from unauthorised or unlawful use of the platform.

## Terms of service

Full terms are available at [revelion.ai/terms](https://revelion.ai/terms).

## Related pages

- [Security Overview](index.md) — platform security architecture
- [Data Handling](data-handling.md) — what data is stored
- [GDPR](gdpr.md) — data protection and your rights
