# UI customization

## Themes

Inji Wallet Mobile currently ships with two theme files:

* `components/ui/themes/DefaultTheme.ts`
* `components/ui/themes/PurpleTheme.ts`

The active theme is selected in `components/ui/styleUtils.ts` from the `APPLICATION_THEME` environment variable:

```ts
import {DefaultTheme} from './themes/DefaultTheme';
import {PurpleTheme} from './themes/PurpleTheme';
import {APPLICATION_THEME} from 'react-native-dotenv';

export const Theme =
  APPLICATION_THEME?.toLowerCase() === 'purple' ? PurpleTheme : DefaultTheme;
```

To add a new theme:

1. Add a new theme file under `components/ui/themes`.
2. Keep the exported object shape compatible with `DefaultTheme` and `PurpleTheme`; `components/ui/themes/themes.test.ts` validates required properties.
3. Import the new theme in `components/ui/styleUtils.ts` and extend the `APPLICATION_THEME` selector.
4. If the splash screen should change with the theme, update `app.config.ts` as well.

## Logos and Background Images

The home header logo is imported by each theme and exposed through the theme object:

```ts
import HomeScreenLogo from '../../../assets/InjiHomeLogo.svg';

export const DefaultTheme = {
  HomeScreenLogo,
  // ...
};
```

`HomeScreenLayout.tsx` renders the header logo through `SvgImage.InjiLogo(Theme.Styles.injiLogo)`, and the logo dimensions/spacing are controlled by `Theme.Styles.injiLogo` and `Theme.Styles.injiHomeLogo`.

The default profile icon is not an image asset. When a credential does not include a face/photo attribute, `components/ProfileIcon.tsx` renders the `person` icon from `react-native-elements` and colors it with `Theme.Colors.ProfileIconColor`:

```tsx
import {Icon} from 'react-native-elements';

<Icon
  name="person"
  color={Theme.Colors.ProfileIconColor}
  size={props.profileIconSize}
/>
```

VC card logos, background colors, text colors, and claims come from the issuer well-known metadata when the issuer provides them. The wallet fetches the issuer metadata through `shared/openId4VCI/Utils.ts` and uses the matching credential configuration for rendering.

If issuer metadata does not provide enough display information, the theme fallback images are used:

```ts
export const DefaultTheme = {
  CloseCard: require('../../../assets/images/png/CardBGLandscape.png'),
  OpenCard: require('../../../assets/images/png/CardBGPortrait.png'),
  // ...
};
```

## Header and Tab Icons

Most app icons are SVG components imported in `components/ui/svg.tsx`. Bottom tab entries are defined in `routes/main.ts`, and the tab renderer in `screens/MainLayout.tsx` resolves each icon through `SvgImage[route.name]`.

For example, the shipped bottom tabs are:

```ts
const home: TabScreen = {
  name: BOTTOM_TAB_ROUTES.home,
  component: HomeScreenLayout,
  icon: 'home',
  options: {
    headerTitle: '',
    headerShown: false,
  },
};
```

To add or replace a tab:

1. Add or replace the route in `routes/main.ts`.
2. Add the matching SVG method in `components/ui/svg.tsx`.
3. Add localized tab labels in the locale JSON files under `locales`.
4. Adjust tab colors, active backgrounds, labels, and spacing in `Theme.BottomTabBarStyle`, `Theme.Styles.bottomTabIconStyle`, and `Theme.Colors.GradientColorsLight`.

## Colors and Typography

Colors and typography are controlled by each theme object. Commonly customized keys include:

| Area | Theme keys |
| --- | --- |
| Bottom tabs | `TabItemText`, `IconBg`, `GradientColorsLight`, `bottomTabIconStyle`, `BottomTabBarStyle` |
| VC card text fallback | `Details`, `DetailsLabel`, `fieldItemTitle`, `fieldItemValue` |
| Buttons and gradients | `gradientBtn`, `linearGradientStart`, `linearGradientEnd`, `LinearGradientDirection` |
| Settings screen | `settingsLabel`, `textLabel`, `textValue`, `AboutInjiScreenStyle` |
| Add credential flow | `IssuersScreenStyles`, `issuerLogo`, `issuersContainer`, `issuersSearchSubText` |
| Status and warnings | `WarningIcon`, `warningLogoBgColor`, `StatusInfoModalStyles`, `ToastItemText` |

Example:

```ts
export const DefaultTheme = {
  Colors: {
    DetailsLabel: Colors.Gray40,
    Details: Colors.Black,
    settingsLabel: Colors.Black,
    textLabel: Colors.Grey,
    // ...
  },
  Styles: StyleSheet.create({
    versionContainer: {
      backgroundColor: Colors.Grey6,
      margin: 4,
      borderRadius: 14,
    },
    // ...
  }),
};
```

## VC Card Customization

VC card rendering is driven first by the credential issuer metadata exposed in the issuer's OpenID4VCI well-known endpoint. The wallet uses this metadata to select display fields and rendering hints for `ldp_vc`, `mso_mdoc`, `vc+sd-jwt`, and `dc+sd-jwt` credentials.

For OpenID4VCI Final 1.0 issuers, the wallet reads `credential_configurations_supported.<credential_configuration_id>.credential_metadata.display` and `credential_metadata.claims`. Legacy issuers that still expose `display`, `claims`, `credential_definition`, or `order` at the top level are handled by fallback parsing.

Issuer display metadata can include name, logo, background color, and text color:

```json
{
  "display": [
    {
      "name": "MOSIP Identity Verifiable Credential",
      "locale": "en",
      "logo": {
        "url": "https://esignet.collab.mosip.net/logo.png",
        "alt_text": "a square logo of a Esignet"
      },
      "background_color": "#FDFAF9",
      "text_color": "#7C4616"
    }
  ]
}
```

If issuer metadata is missing or cannot be parsed, the wallet falls back to the theme defaults described above.
