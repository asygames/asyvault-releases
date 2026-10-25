# AsyVault Privacy Policy

**Effective date: October 25, 2026**  
**Publisher: ASYGAMES**  
**Product: AsyVault for Chrome/Chromium and Firefox**

AsyVault is a local-first encrypted password and developer-secret manager. This policy describes the browser extension's current storage, website integration and network activity.

## 1. Vault data and local encryption
You choose the records to store, including usernames, passwords, notes, cards, identities, API credentials, SSH keys, passkeys and Authenticator configuration. Personal and Developer vault contents are encrypted locally using AES-256-GCM, with keys derived from the master password using PBKDF2-SHA-256. Encrypted snapshots and history are stored in the extension's browser storage and IndexedDB.

The master password is not uploaded to GitHub, backup providers or an ASYGAMES server. Derived unlock keys remain in protected browser-session memory while unlocked and are cleared by locking, expiry, browser restart or extension reload. Optional Authenticator convenience unlock stores a separately encrypted authorization capsule and a non-extractable wrapping key in the authorized browser profile. These device-specific unlock materials are excluded from portable backups and synchronization. This convenience feature is not hardware-backed protection against a compromised browser profile. The original master password is required to authorize a new browser and restore encrypted backups.

## 2. Website assistance and passkeys
AsyVault injects bundled scripts on eligible HTTPS websites after the browser grants the requested site access. The website assistant can inspect login and supported form fields, show matching-account suggestions, fill selected records and offer to save or update credentials. Saving captured credentials requires the extension's confirmation flow. Existing opt-outs and browser site-access restrictions are respected; the website form assistant can be disabled in Settings.

Passkey integration handles supported WebAuthn requests separately from the optional form assistant. After user approval, the requesting website receives the WebAuthn response needed for registration or authentication. Private signing keys remain in the encrypted vault and trusted extension contexts.

Current tab/frame URLs, frame ancestry and Permissions-Policy response headers are processed to check origin, navigation and iframe authorization. A short session diagnostic retains fixed stage/error categories and timestamps for up to five minutes; it does not retain challenge values, credential IDs, account names or private keys. AsyVault does not build a general browsing-history database.

## 3. GitHub and user-configured backups
Current first-run setup for a newly created vault asks the user to connect GitHub to finish setup. Existing or imported vaults can be used locally without reconnecting, and automatic synchronization can be disabled. Connecting uses GitHub OAuth Device Flow with the broad repo scope: the token can technically access other private repositories available to your account. AsyVault's code restricts its own backup operations to your private asyvault-data repository; this restriction is not a GitHub-enforced token boundary.

The GitHub login and OAuth token are stored encrypted locally. GitHub receives authenticated requests, encrypted vault snapshots, repository/commit metadata and routine network metadata, including the source IP address. Disconnecting removes the local authorization; revoking the token or deleting remote repository history is performed in GitHub settings.

Optional secondary encrypted backups can be configured for local downloads, HTTPS/WebDAV, S3-compatible storage or Zipline. A selected remote provider receives encrypted backup files, required authentication and network metadata. Connection settings and credentials are encrypted locally. Remote destinations and retention are controlled by the user and the chosen provider.

On supported Firefox versions, GitHub and secondary-backup transfers also require the optional browser data-transmission consent declared by the extension. Declining transmission leaves new-vault setup unfinished; existing/imported local vault use remains available without enabling cloud backup.

## 4. Website icons and updates
When displaying saved login records, AsyVault may load public favicon.ico or apple-touch-icon.png images directly from their saved HTTPS origins. These requests omit cookies, authentication credentials and referrers and do not contain saved login paths or query strings. The contacted website can observe the request and source IP address. Chromium can also use its browser-native favicon cache; no external icon-aggregation service is used.

Extension updates are managed by the browser's official store mechanism. Optional release-information checks contact GitHub. These checks do not upload vault contents or download executable extension code from GitHub.

## 5. Purpose, recipients and sharing
Data is used to provide vault management, approved website/passkey actions and configured backups. ASYGAMES does not operate a server receiving vault contents, does not sell user data, and does not use it for advertising or data-broker purposes. The extension does not include analytics SDKs or advertising trackers. Websites receive the credentials or passkey responses that the user authorizes for them; chosen backup providers receive the data described above.

GitHub handles its services under its Privacy Statement: https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement. Other selected providers apply their own policies.

## 6. Retention, deletion and recovery
Encrypted records, history and device authorization remain in the local browser profile until removed. Deletion markers prevent stale synchronized copies from restoring deleted active entries, but older snapshots, exports and Git repository history can retain previous encrypted versions. Removing local extension data does not delete external backups.

Encrypted exports contain vault contents and format metadata, not the master password, browser-session unlock keys or OAuth tokens. ASYGAMES cannot reset the master password or recover a vault encrypted with a lost password. No independent security audit is claimed for this release.

## 7. Browser permissions
- storage: encrypted vaults, settings and protected session state.
- alarms: background scheduling, retry and session expiry.
- scripting and HTTPS site access: website assistance and WebAuthn integration.
- contextMenus: user-invoked vault shortcuts.
- clipboardWrite: user-selected copy actions.
- webNavigation: browser-verified frame ancestry and navigation state for secure passkey routing.
- webRequest: observation of page/frame response policy headers for WebAuthn authorization; this feature does not modify traffic or read request bodies.
- favicon, on Chromium: browser-native cached site icons.
- downloads, optional: user-enabled local encrypted backup downloads.

The manifest declares broad HTTPS site access. Firefox also declares optional authentication, personal, financial/payment, browsing-activity and website-content data categories for encrypted backup transfers.

## 8. Changes and contact
This policy is updated when functionality or data practices change. Contact the maintainer through https://github.com/asygames/asyvault-releases/issues/new. Do not put passwords, access tokens, recovery codes, private keys or personal vault exports in a public support issue.
