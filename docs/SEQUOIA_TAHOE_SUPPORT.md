# macOS Sequoia (15.0+) and Tahoe (26.0+) Support

## Overview

Starting with macOS Sequoia (15.0), Apple changed how the BeaconStore encryption key is stored in the keychain. This affects FindMySync's ability to automatically decrypt FindMy data.

## Automatic Key Extraction

FindMySync now includes automatic support for macOS Sequoia and Tahoe. The app will attempt to extract the BeaconStore key using multiple methods:

1. **User Preferences**: If you've manually entered a key in the Extras panel
2. **Service Attribute Method** (macOS 15.0+): Uses `kSecAttrService` for Sequoia/Tahoe compatibility
3. **Label Attribute Method**: Fallback for older macOS versions
4. **Command Line Method**: Uses `/usr/bin/security` command

## Manual Key Extraction

If automatic extraction fails, you may need to manually extract the key:

### Method 1: Using beaconstorekey-extractor (Recommended)

For detailed instructions, visit: https://github.com/pajowu/beaconstorekey-extractor

**Warning**: This method requires temporarily disabling System Integrity Protection (SIP). Follow the instructions carefully.

Quick steps:
1. Disable SIP (see repository instructions)
2. Clone and build the extractor:
   ```bash
   git clone https://github.com/pajowu/beaconstorekey-extractor.git
   cd beaconstorekey-extractor
   make run
   ```
3. Copy the extracted key
4. Re-enable SIP
5. Paste the key in FindMySync's Extras panel

### Method 2: Using Terminal Command

1. Open Terminal
2. Run:
   ```bash
   /usr/bin/security find-generic-password -l BeaconStore -g
   ```
3. Look for the "gena" value (hex string like `0xABCDEF...7890`)
4. Copy the hex string (without spaces)
5. Paste it in FindMySync's Extras panel under "Beacon decrypt key"

## Troubleshooting

### Key Not Found
- Ensure FindMy app is running and has cached data
- Try restarting the FindMy app
- Check that you're signed in to iCloud

### Permission Denied
- Grant FindMySync full disk access in System Preferences
- On Sequoia/Tahoe, you may need to manually extract the key

### Data Still Not Decrypting
- Verify the key is entered correctly (no spaces, include "0x" prefix if present)
- Check the Status panel for detailed error messages
- Try force updating from the Status panel

## Technical Details

The BeaconStore key is used to decrypt AES-GCM encrypted files in:
- `~/Library/com.apple.icloud.searchpartyd/BeaconNamingRecord`
- `~/Library/com.apple.icloud.searchpartyd/BeaconEstimatedLocation`
- `~/Library/com.apple.icloud.searchpartyd/OwnedBeacons`

On macOS Sequoia and later, the key requires the `com.apple.icloud.searchpartyuseragent` keychain access group entitlement, which is why manual extraction may be necessary.

## References

- [Issue #40: macOS Sequoia Support](https://github.com/MartinPham/FindMySync/issues/40)
- [Issue #47: Solution using beaconstorekey-extractor](https://github.com/MartinPham/FindMySync/issues/47)
- [beaconstorekey-extractor Repository](https://github.com/pajowu/beaconstorekey-extractor)
