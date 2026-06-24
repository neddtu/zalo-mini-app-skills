# Permission & Biometric APIs

## Permission Settings

Use `getSetting` to inspect permissions and `openPermissionSetting` to let users adjust permissions.

```ts
import { getSetting, openPermissionSetting } from "zmp-sdk/apis";

const settings = await getSetting({});
if (!settings["scope.userLocation"]) {
  await openPermissionSetting({});
}
```

Use a clear in-app explanation before opening permission settings.

## requestSendNotification

Ask for permission to send notifications where product flow needs it.

```ts
import { requestSendNotification } from "zmp-sdk/apis";

await requestSendNotification({});
```

Use only after user action. Do not ask on first app load unless app purpose requires it.

## requestUpdateZalo

Prompt user to update Zalo when a required native capability is unavailable.

```ts
import { requestUpdateZalo } from "zmp-sdk/apis";

await requestUpdateZalo({});
```

## Biometric Authentication

Docs include biometric integration APIs:

- `checkStateBioAuthentication`
- `openBioAuthentication`

```ts
import { checkStateBioAuthentication, openBioAuthentication } from "zmp-sdk/apis";

const state = await checkStateBioAuthentication({});
if (state?.available) {
  const result = await openBioAuthentication({
    reason: "Confirm this action"
  });
}
```

Security notes:

- Biometrics confirm local user presence; they are not backend identity proof by themselves.
- Pair biometric success with server-side session/auth checks for sensitive actions.
- Provide fallback PIN/password/OTP if product requires access recovery.

Official docs: https://miniapp.zaloplatforms.com/documents/api/biometric-authentication-integration/
