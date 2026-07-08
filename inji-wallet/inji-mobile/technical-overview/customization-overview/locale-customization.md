# Locale customization

Inji Wallet Mobile uses `i18next`, `react-i18next`, and `expo-localization`. Locale resources live in the top-level `locales` folder in the mobile wallet repo, and `i18n.ts` wires those resources into the app.

## Supported Languages

The mobile codebase currently imports these resource files:

| App code | Resource file | Language |
| --- | --- | --- |
| `en` | `locales/en.json` | English |
| `fil` | `locales/fil.json` | Filipino |
| `ar` | `locales/ara.json` | Arabic |
| `hi` | `locales/hin.json` | Hindi |
| `kn` | `locales/kan.json` | Kannada |
| `ta` | `locales/tam.json` | Tamil |

## Add a New Language

1. Add a JSON resource file under `locales`, using the same namespaces and keys as `locales/en.json`.
2. Import the file in `i18n.ts`.
3. Add the imported resource to the `resources` object.
4. Add the app language code and display label to `SUPPORTED_LANGUAGES`.
5. Add translated issuer display data in `mimoto-issuers-config.json` where the Add New Card screen should show issuer names, titles, and descriptions in the new language.

Example:

```ts
import fr from './locales/fra.json';

const resources = {en, fil, ar, hi, kn, ta, fr};

export const SUPPORTED_LANGUAGES = {
  en: 'English',
  fil: 'Filipino',
  ar: 'Arabic',
  hi: 'Hindi',
  kn: 'Kannada',
  ta: 'Tamil',
  fr: 'French',
};
```

The display labels in `SUPPORTED_LANGUAGES` can be localized; keep the object keys aligned with the resource keys.

Use translations through `useTranslation` or the existing `i18n.t` helpers:

```tsx
const {t} = useTranslation('common');

<Text>{t('editLabel')}</Text>;
```

## Language Codes in Issuer Metadata

The wallet uses two-letter language codes internally, but issuer and credential metadata may use either two-letter or three-letter codes. `i18n.ts` builds a language-code map using the `iso-639-3` package so fields such as issuer display names and localized credential values can match either form.

When adding issuer display entries in `mimoto-issuers-config.json`, keep the `language` values consistent with the app language codes where possible:

```json
{
  "display": [
    {
      "name": "Example Issuer",
      "title": "Download Example Credential",
      "description": "Download example credential",
      "language": "en"
    }
  ]
}
```

For OpenID4VCI well-known credential metadata, use the issuer's `locale` or localized claim metadata according to the OpenID4VCI specification. The wallet falls back to English, `en-US`, or the first available entry when a language-specific display entry is not found.

## About libraries

1. [i18next](https://www.i18next.com/)
2. [react-i18next](https://react.i18next.com/)
3. [expo-localization](https://docs.expo.dev/versions/latest/sdk/localization/)

* Inji Wallet has the capability to support multiple languages.
* `i18next` is an internationalization framework. It provides the standard i18n features such as [plurals](https://www.i18next.com/translation-function/plurals), [context](https://www.i18next.com/translation-function/context), [interpolation](https://www.i18next.com/translation-function/interpolation), and [format](https://www.i18next.com/translation-function/formatting). It provides a complete solution to localize products from the web to mobile and desktop.
* `react-i18next` is a set of components, hooks, and plugins that sit on top of i18next, and is specifically designed for React.
* `expo-localization` allows you to localize the app, customizing the experience for specific regions, and languages. It also provides access to the locale data on the native device.
