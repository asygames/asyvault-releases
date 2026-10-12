# AsyVault Privacy Policy

**Effective date: October 12, 2026**  
**Publisher: ASYGAMES**  
**Product: AsyVault browser extension (Chrome / Chromium-based browsers)**

AsyVault is a local-first encrypted vault for personal credentials, developer secrets, usernames, site/project URLs, and private notes. This policy explains what the extension stores, when it communicates with GitHub, and how you can manage that information.

## 1. Information you choose to store

When you create a vault, you can save account names, usernames, passwords, API credentials, project identifiers, URLs, notes, and other text you explicitly enter. AsyVault encrypts the Personal and Developer vaults locally using AES-256-GCM. The keys are derived from your master password using PBKDF2-SHA-256.

Your master password is **not uploaded to GitHub or to an ASYGAMES server**. AsyVault cannot reset it or recover data encrypted with a lost master password. The extension temporarily retains *derived encryption key material* in memory-backed browser session storage while your vault is unlocked; this session material is cleared when the browser session ends or you manually lock the vault.

Encrypted vault data remains in your browser's extension-local storage unless you choose to export a backup or enable GitHub synchronization.

## 2. Optional GitHub authorization and synchronization

GitHub synchronization is optional. If you choose **Connect with GitHub**, AsyVault uses the official GitHub OAuth Device Flow and requests the `repo` permission. This permission is **broad**: a GitHub OAuth token with `repo` scope can technically access other private repositories available to your GitHub account. The current AsyVault client code deliberately restricts its own backup requests to your private `asyvault-data` repository, but this is **not a server-enforced restriction on the OAuth token**.

After authorization, the extension obtains your GitHub login name and an OAuth access token. The access token is stored **encrypted locally** inside the extension and sent to GitHub over HTTPS when you request backup/synchronization. The extension requests or creates a private repository named `asyvault-data` on your account and transmits **encrypted vault snapshots**, not plaintext vault entries. GitHub receives the encrypted file, repository paths, commit metadata, account/login and network request metadata. Previous encrypted snapshots may remain accessible in Git repository history, even after an entry is deleted from current snapshots.

ASYGAMES does **not** operate a separate server receiving your vault contents or the OAuth access token. GitHub operates its own service and handles requests under its [Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement).

You can disconnect GitHub within AsyVault to delete the locally stored OAuth credential. Disconnecting does **not** revoke the token at GitHub, remove the remote backup, or delete its commit history. To revoke access, visit [GitHub Authorized OAuth Apps](https://github.com/settings/applications); to delete the encrypted backup, delete your `asyvault-data` repository through your GitHub account.

## 3. Exporting and importing your encrypted vault

AsyVault can export an encrypted `.asyvault` backup to a location you choose. The exported file contains both encrypted vaults and basic file metadata such as format and export time; it does **not** contain your master password, browser-session keys, or GitHub OAuth access token. You can import this file in another compatible browser, using the original master password to verify and decrypt the vault. Backups stored outside AsyVault remain under your control.

## 4. Network access and update checks

AsyVault communicates with `github.com` for optional OAuth authorization and `api.github.com` for optional encrypted sync, repository verification, and on-demand release/update checks. These requests necessarily disclose IP addresses and routine request metadata to GitHub. Checking release information does not upload vault entries or secrets. Chrome Web Store updates are handled by the browser's ordinary extension update mechanism.

AsyVault does **not** inject scripts into sites, read the contents of webpages you visit, or collect browsing history. It does not use analytics SDKs, advertising trackers, or telemetry endpoints in the current release.

## 5. Use and sharing of data

AsyVault uses the information you enter solely to provide encrypted vault storage, optional encrypted backups/sync, and the other user-requested features described above.

ASYGAMES does **not** sell vault data, use it for advertising, share it with data brokers, or disclose user secrets to third parties. When you explicitly enable GitHub synchronization, encrypted snapshots and required request metadata are sent **to GitHub as a service provider you choose**. ASYGAMES staff do not have a system to view or decrypt your vault.

## 6. Retention, deletion and security

Local encrypted records remain in extension storage until you delete them or remove the extension's local data. A record deleted through AsyVault is excluded from active lists and marked as deleted for sync, but older encrypted snapshots or exported backups can still contain earlier versions. Google Chrome or other browsers may retain or delete extension storage according to their own policies when extensions are removed.

Remote GitHub backups remain on your GitHub account until you remove them. GitHub commit history may retain previous encrypted versions. We do not independently control GitHub's retention of repository data or service metadata.

The current implementation uses browser WebCrypto APIs, AES-GCM encryption, and HTTPS communication. **AsyVault is experimental software without an independent security audit**. Do not rely on it as the sole storage location for critical recovery information or production secrets.

## 7. Permissions

- **`storage`**: saves encrypted local vaults, protected OAuth tokens, and ephemeral session key material required to unlock during a browser session.
- **`https://github.com/*`**: used for the GitHub OAuth Device Flow during optional account connection.
- **`https://api.github.com/*`**: used for optional encrypted backup/sync and for checking public release information when requested.

AsyVault does not request blanket webpage reading or browsing-history permissions.

## 8. Changes to this policy

We will update this page when the extension's data practices or features materially change. The effective date above will be revised, and the updated policy will be available at the same public URL.

## 9. Contact

For privacy-related questions or deletion instructions, contact the project maintainer through the public [AsyVault Releases support issues](https://github.com/asygames/asyvault-releases/issues/new).

**Do not publish passwords, access tokens, recovery codes, or personal secrets in a public support issue.**
