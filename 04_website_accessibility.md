# Website - Accessibility

EmberJS is is committed to ensuring that its website is accessible to people with disabilities. All the pages on our website will meet W3C WAI’s Web Content Accessibility Guidelines 2.1, Level AA conformance. Please report any issues at https://github.com/ember-learn/ember-website/issues.

## Design

These are the WCAG conformance criteria that will most likely apply to the Ember.js website.

<!--alex ignore Color-->
- 1.4.1 [Use of Color](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141#distinguishable)
- 1.4.3 [Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141#contrast-minimum)
- 1.4.4 [Resize Text](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144#resize-text)
  - designs should consider that elements will be coded to support zoom- what should the design look like when a user zooms in (on any device)?
  - Note that the current success criteria is to support zoom between 100%-200%. The newest edition of WCAG success criteria indicates support for zoom from 100%-400%.
- 1.4.5 [Images of Text](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144%2C145#images-of-text) (TL;DR- there shouldn’t be text on a website that is an image. Use text).
- 1.4.8 [Visual Presentation](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144%2C145%2C146#visual-presentation) (AAA so optional, but some are good practice so worth reviewing)
- 1.4.10 [Reflow](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144%2C145%2C146#reflow)
- 1.4.13 [Content on Hover or Focus](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144%2C145%2C146%2C148%2C23%2C246%2C2410%2C323#content-on-hover-or-focus)
- 2.3 [Seizures and Physical Reactions]() (related to anything that is animated)
- 2.4.6 [Headings and Labels](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144%2C145%2C146%2C148%2C23#seizures-and-physical-reactions) (designers: make sure everything has a heading, or provide a machine-readable heading for developers to implement if visually hidden)
- 3.2.3 [Consistent Navigation](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=141%2C143%2C144%2C145%2C146%2C148%2C23%2C246#consistent-navigation)

## Development

(WIP)