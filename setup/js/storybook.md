[#]() storybook basic notes
## install
```bash
pnpm dlx storybook@latest init
```
## config
### main
```javascript
/** @type { import('@storybook/html-vite').StorybookConfig } */
const config = {
  staticDirs: ['../../../public/'],
  stories: ['../src/**/*.mdx', '../src/**/*.stories.@(js|jsx|mjs|ts|tsx)'],
  addons: [
    '@storybook/addon-links',
    '@storybook/addon-essentials',
    '@storybook/addon-interactions',
    "@storybook/addon-themes",
    '@storybook/addon-a11y',
  ],
  framework: {
    name: '@storybook/html-vite',
    options: {},
  },
  docs: {
    autodocs: 'tag',
  },
}
export default config
```
### preview
```javascript

import '../dev.css'
import { withThemeByDataAttribute } from "@storybook/addon-themes";

/** @type { import('@storybook/html').Preview } */
const preview = {
  parameters: {
    actions: { argTypesRegex: '^on[A-Z].*' },
    controls: {
      matchers: {
        color: /(background|color)$/i,
        date: /Date$/i,
      },
    },
  },
}

export const decorators = [
  withThemeByDataAttribute({
    themes: {
      light: "light",
      dark: "dark",
    },
    defaultTheme: "light",
    attributeName: "data-theme",
  }),
];

export default preview
```

### manager
```javascript
import { addons } from '@storybook/manager-api';
import { create } from '@storybook/theming';

addons.setConfig({
  theme: create({
    base: 'dark',
    brandTitle: 'Alief Prihantoro',
    brandUrl: 'https://alifprihantoro.netlify.com',
    brandImage: '/favicon-32x32.png',
    brandTarget: '_self',
  }),
});
addons.setConfig({
  /**
   * theme storybook, see link below
   * https://storybook.js.org/docs/configure/theming#create-a-theme-quickstart
   */
  theme: create({
    base: 'dark',
    brandTitle: 'Alief Prihantoro',
    brandUrl: 'https://alifprihantoro.netlify.com',
    brandImage: '/favicon-32x32.png',
    brandTarget: '_self',
  }),
  
  /**
   * sidebar config
   */
  sidebar: {
    showRoots: false,
  },
  /**
   * show story component as full screen
   * @type {Boolean}
   */
  isFullscreen: false,

  /**
   * display panel that shows a list of stories
   * @type {Boolean}
   */
  showNav: true,

  /**
   * display panel that shows addon configurations
   * @type {Boolean}
   */
  showPanel: true,

  /**
   * where to show the addon panel
   * @type {('bottom'|'right')}
   */
  panelPosition: 'bottom',

  /**
   * sidebar tree animations
   * @type {Boolean}
   */
  sidebarAnimations: true,

  /**
   * enable/disable shortcuts
   * @type {Boolean}
   */
  enableShortcuts: true,

  /**
   * show/hide tool bar
   * @type {Boolean}
   */
  isToolshown: true,

  /**
   * id to select an addon panel
   * @type {String}
   */
  selectedPanel: undefined,
});
```

## write story
```typescript

import Component from './'

// More on how to set up stories at: https://storybook.js.org/docs/html/writing-stories/introduction
export default {
  title: 'Components/Title',
  tags: ['autodocs'],
  args: {
    index: 1,
  },
  // see https://storybook.js.org/docs/api/arg-types
  argTypes: {
    index: {
      control: 'select',
      options: [1, 2, 3, 4],
    },
  },
  render: ({ index, content }: { index: number, content: string | string[] }) => {
    return `<div class="bg-base-100">${Component(index, content)}</div>`
  },

}
export const Contact = {}
export const Contact2 = {}
```
