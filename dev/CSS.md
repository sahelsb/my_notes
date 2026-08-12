
### Styling architecture: Tailwind, shadcn/ui and design tokens

#### 1. Tailwind CSS — styling by utility classes

Instead of writing CSS in a separate file, you put small single-purpose classes directly in the
markup:

  ```bash
  <div className="flex items-center gap-3 rounded-lg border p-4">

  flex = display:flex, gap-3 = a fixed gap, p-4 = padding. Each class does one thing. There's no
  .card { … } block anywhere — the styling lives at the point of use.
  ```


#### 2. Radix UI — behavior without looks

  Some components are hard to build correctly: dropdowns, tabs, popovers, selects. They need keyboard
  navigation, focus management, screen-reader labels, click-outside handling.

  Radix provides exactly that behavior — and no styling at all. A Radix tab is fully functional and
  completely invisible. You bring the appearance.


#### 3. shadcn/ui — the part people misunderstand

  shadcn/ui is not a component library you install as a dependency. There is no import { Button } 
  from 'shadcn'.

  It's a collection of source files you copy into your own project. They are Radix (behavior) +
  Tailwind classes (appearance), pre-assembled. Once copied, they are your files — you edit them like
  any other code.


#### 4. Design tokens — the actual concept

  A token is a named value, defined once, referenced everywhere:

  ```bash
  --primary: #7b6039;
  --border:  #e6dfd2;
  ```

  The rule that makes it work: components never name a color. They only name a token.

```bash
  // button.tsx — refers to a name, not to brown
  'bg-primary'
```

  So the appearance of the whole app is decided in one place — the token list — not scattered across
  50 components.

#### 5. Theming = redefining the tokens

  Because everything points at names, you change the app's look by changing what the names mean:

```bash
  /* before */  --primary: oklch(0.205 0 0);   /* grey */
  /* after  */  --primary: #7b6039;            /* brown */
```

  Every button, badge, focus ring and progress bar that referenced --primary changes at once. No
  component is edited.

