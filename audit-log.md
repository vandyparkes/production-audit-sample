# Audit log

## 1. Semantic HTML

1. Area: Semantic HTML.
2. Condition: `index.html` line 2, Chrome, viewport 1920×1080, zoom scale 1. Document element.
3. Finding: The root element is `<html>` with no `lang` attribute. `document.documentElement.lang` is `""`. `hasAttribute("lang")` is false.
4. Evidence: The W3C Nu Html Checker reported: Consider adding a "lang" attribute to the "html" start tag to declare the language of this document. MDN `lang`: the language is in an unknown state if there is no indication of language anywhere. https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/lang
5. Impact: A screen reader has no page language to use for pronunciation.
6. Priority: High. The language of the whole page is unknown.

## 2. CSS responsiveness

1. Area: CSS responsiveness.
2. Condition: `styles.css` line 54 and line 141, Chrome, viewport 390px wide, zoom scale 1. `matchMedia` and computed width.
3. Finding: `.page` is `width: 1180px`. `@media (max-width: 900px)` changes `.hero` to one column and does not change `.page`.
4. Evidence: `matchMedia("(max-width: 900px)")` was true. Computed `.page` width stayed `1180px`. `scrollWidth` was 1180 and `clientWidth` was 375. The hero computed to one column, `1116px`. The W3C CSS Validator reported `styles.css` valid, with 0 errors. MDN Using media queries: a `max-width` query applies the styles inside it only when the viewport is that width or narrower. https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Media_queries/Using_media_queries
5. Impact: A narrow window has to scroll sideways to see the page.
6. Priority: High. The page is 1180px wide in a 390px viewport.

## 3. Accessibility

1. Area: Accessibility.
2. Condition: `schedule.html` lines 26–28, Chrome, viewport 1920×1080, zoom scale 1. Accessibility tree.
3. Finding: Time, Session, and Room are `td` elements. The accessibility tree reports each one as `cell`. The table has 0 `th` elements.
4. Evidence: The W3C Nu Html Checker reported no messages for `schedule.html`. MDN `th`: the `th` element defines a cell as the header of a group of table cells. Its implicit ARIA role is `columnheader` or `rowheader`. https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/th
5. Impact: A screen reader does not get Time, Session, and Room as column headers.
6. Priority: Medium. The cell text is present, and the header role is not.

## 4. Links

1. Area: Links.
2. Condition: `schedule.html` line 16, Chrome, viewport 1920×1080, zoom scale 1. Register link, then Enter.
3. Finding: Register points to `registration.html`. Chrome opened that URL and showed Error code: 404, Message: File not found.
4. Evidence: The response status was `404 File not found`. The W3C Nu Html Checker reported no messages for `schedule.html`. MDN 404 Not Found: the server cannot find the requested resource. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/404
5. Impact: Register on the schedule page opens an error page.
6. Priority: High. The link target is missing.
