# Clean my Mac

1. User cache files

On finder (Desktop menu) Go to Folder
~/Library/Caches
remove all files and dirs inside of Caches dir

2. Xcode Derived data

~/Library/Developer/Xcode/DerivedData
~/Library/Developer/Xcode/iOS Device Logs

3. User log files

~/Library/Logs

## Remove Unused Simulators Manually

### Option 1: Delete Unused Simulators via Xcode

1. Open **Xcode**.
2. Go to **Window** > **Devices and Simulators**.
3. Select **old/unneeded** simulators.
4. Click the "**–**" (minus) button to delete them.

### Option 2: Remove Simulators via Terminal

To remove all unused simulator files:

```bash
xcrun simctl delete unavailable
```

This will delete all orphaned simulators no longer linked to the current Xcode version.

### Option 3: Manually Delete from Finder

1. Open **Finder**.
2. Go to `~/Library/Developer/CoreSimulator/Devices/`
3. Delete old simulator folders (compare with Xcode’s list to avoid removing active ones).

### Final Cleanup (If required)

After deleting, free up even more space by running:

```bash
xcrun simctl erase all
```

This will reset all remaining simulators to a clean state.
