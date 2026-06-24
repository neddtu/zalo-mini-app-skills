# Device, Media & Document APIs

Use from `zmp-sdk/apis`.

## Location

### getLocation

Requires user permission and app approval for production.

```ts
import { getLocation } from "zmp-sdk/apis";

const { latitude, longitude, accuracy } = await getLocation({});
```

Request only when location is essential. Provide fallback manual address input.

## Camera

### createCameraContext

```ts
import { createCameraContext } from "zmp-sdk/apis";

const camera = createCameraContext();
await camera.start({
  targetElement: document.getElementById("camera-view"),
  facing: "back"
});

const photo = await camera.takePhoto({});
await camera.stop();
```

Camera context methods in current docs include:

- `start()` / `stop()`
- `pause()` / `resume()`
- `takePhoto()`
- `flip()`
- `setMirror()`
- `on()` / `off()` events
- `getCameraList()`
- `getSelectedDeviceId()`
- `setDeviceId()`
- `isUsing()`
- `updateMediaConstraints()`

### requestCameraPermission / checkZaloCameraPermission

```ts
import { requestCameraPermission, checkZaloCameraPermission } from "zmp-sdk/apis";

const status = await checkZaloCameraPermission({});
if (!status?.granted) {
  await requestCameraPermission({});
}
```

Verify exact return shape in installed `zmp-sdk` types.

## File & Media

### chooseImage

Legacy/simple image picker.

```ts
import { chooseImage } from "zmp-sdk/apis";

const { tempFilePaths } = await chooseImage({
  count: 9,
  sourceType: ["album", "camera"]
});
```

### openMediaPicker: Current Shape

Current docs use `maxSelectItem` and return `{ data }`.

```ts
import { openMediaPicker } from "zmp-sdk/apis";

const { data } = await openMediaPicker({
  type: "photo",
  maxSelectItem: 5,
  serverUploadUrl: "https://example.com/upload",
  compressLevel: "medium"
});
```

Common `type` values in current docs:

- `photo`
- `video`
- `file`
- `zcamera`
- `zcamera_photo`
- `zcamera_video`
- `zcamera_scan`

Avoid outdated examples using `type: "image"`, `maxSelection`, or `{ files }` unless project package types prove compatibility.

Official docs: https://miniapp.zaloplatforms.com/documents/api/openMediaPicker/

### saveImageToGallery / saveVideoToGallery

```ts
import { saveImageToGallery, saveVideoToGallery } from "zmp-sdk/apis";

await saveImageToGallery({ imageUrl: "https://example.com/image.jpg" });
await saveVideoToGallery({ videoUrl: "https://example.com/video.mp4" });
```

## Documents & Downloads

### downloadFile

Download remote file for later local use.

```ts
import { downloadFile } from "zmp-sdk/apis";

const result = await downloadFile({ url: "https://example.com/file.pdf" });
```

### openDocument

Open a PDF/document from remote or local file depending on supported options.

```ts
import { openDocument } from "zmp-sdk/apis";

await openDocument({
  url: "https://example.com/file.pdf"
});
```

Docs mention modes like viewing/downloading/editing depending on file type and platform support. Verify exact args in project SDK types.

Official docs: https://miniapp.zaloplatforms.com/documents/api/openDocument/

## Scanning

### scanQRCode

```ts
import { scanQRCode } from "zmp-sdk/apis";

const { content } = await scanQRCode({});
```

### scanNFC / checkNFC

```ts
import { checkNFC, scanNFC } from "zmp-sdk/apis";

const nfc = await checkNFC({});
if (nfc?.available) {
  const { data } = await scanNFC({});
}
```

## Network

### getNetworkType / onNetworkStatusChange

```ts
import { getNetworkType, onNetworkStatusChange } from "zmp-sdk/apis";

const { networkType } = await getNetworkType({});

onNetworkStatusChange((status) => {
  console.log(status);
});
```

## Screen & Haptics

```ts
import { keepScreen, vibrate } from "zmp-sdk/apis";

await keepScreen({ on: true });
await vibrate({});
```
