# Local File Storage APIs

Local File Storage (LFS) stores files locally on the user's device for Mini App reuse.

Official docs: https://miniapp.zaloplatforms.com/documents/api/localFileSystem/

## Support Check

Docs note LFS support begins around `zmp-sdk@2.51.0` and newer Zalo app versions. Check support at runtime.

```ts
import { isSupportLFS } from "zmp-sdk/apis";

const { isSupported } = await isSupportLFS({});
if (!isSupported) {
  // fallback: remote URL, normal cache, or ask user to update Zalo
}
```

Verify exact return shape in installed SDK types.

## saveFile

Save a temporary/downloaded file into local file storage.

```ts
import { saveFile } from "zmp-sdk/apis";

const saved = await saveFile({
  tempFilePath: "local-temp-path-or-downloaded-path"
});
```

## getFileInfo

```ts
import { getFileInfo } from "zmp-sdk/apis";

const info = await getFileInfo({
  filePath: "saved-file-path"
});
```

## getSavedFileList

```ts
import { getSavedFileList } from "zmp-sdk/apis";

const list = await getSavedFileList({});
```

## removeSavedFile

```ts
import { removeSavedFile } from "zmp-sdk/apis";

await removeSavedFile({
  filePath: "saved-file-path"
});
```

## Implementation Guidance

- Treat LFS as cache, not authoritative storage.
- Keep server copy for important documents.
- Add cache invalidation by app version/user id/data version.
- Provide fallback for unsupported devices/Zalo versions.
- Avoid storing sensitive documents unless encrypted/server policy allows.
