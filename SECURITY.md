# Security Policy

## Supported Versions
| Version | Supported |
|---------|-----------|
| 1.0.x   | yes       |

## Reporting a Vulnerability
Open a private security advisory on GitHub or email the maintainers. Do not disclose publicly before a fix is available.

## Security Principles in this Project
- All imported JSON is treated as untrusted input
- No `eval`, `new Function`, `innerHTML` with user data
- All rendered text uses `textContent` or Canvas `fillText` with escaped values
- Color values validated against hex/rgba pattern
- Numeric ranges clamped to schema limits
- Canvas dimensions capped (max 8192x8192) to prevent memory exhaustion
- File sizes limited to 50MB for imports
- Project duration capped at 3600s
- Object/ track references validated before render
- URL assets must be same-origin or CORS-enabled; external scripts never executed

## Validated Fields
Protocol version, required properties, numeric ranges, color formats, track/object references, keyframe times, effect IDs, file sizes, canvas dimensions, resource limits.

## Dependencies
This project has no runtime npm dependencies for the main app. All rendering is browser-native.

## Best Practices for Users
- Only import JSON from trusted AI outputs you have reviewed
- Review imported projects in the JSON editor before rendering
- Exported videos are generated locally; no data leaves your browser
