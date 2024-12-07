# UI Settings Overlay Component

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This component handles the UI settings overlay, allowing users to customize their settings.</p>
  <img src="uisettingsoverlay.png" alt="Flowchart of UI Settings Overlay Component"/>
</tldr>

<procedure title="To manage UI settings:" id="procedure-id-ui-settings">
   <step>Initialize the settings store and retrieve the current settings.</step>
   <step>Render the UI settings overlay with options for customization.</step>
   <step>Handle user interactions and update the settings store accordingly.</step>
   <step>Persist the updated settings and apply changes to the UI.</step>
   <p>Congratulations! You have successfully managed the UI settings overlay.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a> !</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the settings store is correctly initialized and managed.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the execution of the component.

## Sequence and Flow

1. **Import Dependencies**:
- The necessary modules and utilities are imported, including `useSettingsStore`, `Image`, `Select`, `Label`, and `useTranslate`.

2. **Initialize Settings Store**:
- The settings store is initialized and the current settings are retrieved.

3. **Render UI Settings Overlay**:
- The UI settings overlay is rendered with options for customization, including language selection.

4. **Handle User Interactions**:
- User interactions are handled, updating the settings store accordingly.

5. **Persist and Apply Settings**:
- The updated settings are persisted and applied to the UI.

<img src="sequence.png" alt="Sequence Diagram of UI Settings Overlay Component"/>

## Example Code

```typescript
import useSettingsStore from "@/stores/settingsStore";
import Image from "next/image";
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";
import { Label } from "@/components/ui/label";
import { languages, useTranslate } from "@/lib/translate";

export default function UITab() {
  const { t } = useTranslate();
  const lang = useSettingsStore((s) => s.language);
  const setLang = useSettingsStore((s) => s.setLanguage);

  return (
    <div className="flex flex-col gap-2">
      <div className="flex flex-col justify-between gap-2">
        <Label htmlFor="language">{t("language")}</Label>
        <Select value={lang} onValueChange={setLang}>
          <SelectTrigger>
            <SelectValue placeholder={t("overlay.settings.ui.selectLanguage")} />
          </SelectTrigger>
          <SelectContent>
            {languages.map((lang) => (
              <SelectItem key={lang} value={lang}>
                <div className="flex items-center gap-2">
                  <Image
                    src={`/assets/img/flags/${lang}.webp`}
                    alt={`${lang} flag`}
                    width={24}
                    height={16}
                    className="object-cover"
                  />
                  <span>{t(`languages.${lang}`)}</span>
                </div>
              </SelectItem>
            ))}
          </SelectContent>
        </Select>
      </div>
    </div>
  );
}