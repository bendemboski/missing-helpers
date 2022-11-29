# missing-helpers

This app demonstrates [issue #1296](https://github.com/embroider-build/embroider/issues/1296). To see the error, run `ember serve` and visit `http://localhost:4200`.

It should render `before basic dropdown trigger after basic dropdown`, but instead renders `before basic dropdown`. This is because `trigger` is the trigger of a `<BasicDropdown>` and as can be seen in the console, rendering it causes an assertion:

```
Error occurred:

- While rendering:
  -top-level
    application
      BasicDropdown


execute @ vendor.js:46109
vendor.js:36004 Uncaught Error: Attempted to resolve `ensure-safe-component`, which was expected to be a helper, but nothing was found.
    at resolveHelper (vendor.js:36004:15)
    at encodeOp (vendor.js:38335:18)
    at pushOp (vendor.js:38249:7)
    at vendor.js:36273:7
    at Compilers.compile (vendor.js:36248:7)
    at expr (vendor.js:36455:19)
    at Curry (vendor.js:36700:5)
    at vendor.js:36287:5
    at Compilers.compile (vendor.js:36248:7)
    at expr (vendor.js:36455:19)
```

`application.hbs` successfully invokes a helper directly, and its compiled form (`application.hbs`) is:

```js
__webpack_require__.r(__webpack_exports__);
/* harmony export */ __webpack_require__.d(__webpack_exports__, {
/* harmony export */   "default": () => (__WEBPACK_DEFAULT_EXPORT__)
/* harmony export */ });
/* harmony import */ var _externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ../../externals/@ember/template-factory */ "../externals/@ember/template-factory.js");
/* harmony import */ var _externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0___default = /*#__PURE__*/__webpack_require__.n(_externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0__);
/* harmony import */ var _components_basic_dropdown_js__WEBPACK_IMPORTED_MODULE_1__ = __webpack_require__(/*! ../components/basic-dropdown.js */ "./components/basic-dropdown.js");
/* harmony import */ var _helpers_or_js__WEBPACK_IMPORTED_MODULE_2__ = __webpack_require__(/*! ../helpers/or.js */ "./helpers/or.js");
/* harmony import */ var _helpers_page_title_js__WEBPACK_IMPORTED_MODULE_3__ = __webpack_require__(/*! ../helpers/page-title.js */ "./helpers/page-title.js");




/* harmony default export */ const __WEBPACK_DEFAULT_EXPORT__ = ((0,_externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0__.createTemplateFactory)(
/*
  {{page-title "MissingHelpers"}}

{{or "before basic dropdown" ""}}

<BasicDropdown as |dd|>
  <dd.Trigger>
    trigger
  </dd.Trigger>
  <dd.Content>
    content
  </dd.Content>
</BasicDropdown>

after basic dropdown

{{outlet}}
*/
{
  "id": "UjC0Pf3S",
  "block": "[[[1,[28,[32,0],[\"MissingHelpers\"],null]],[1,\"\\n\\n\"],[1,[28,[32,1],[\"before basic dropdown\",\"\"],null]],[1,\"\\n\\n\"],[8,[32,2],null,null,[[\"default\"],[[[[1,\"\\n  \"],[8,[30,1,[\"Trigger\"]],null,null,[[\"default\"],[[[[1,\"\\n    trigger\\n  \"]],[]]]]],[1,\"\\n  \"],[8,[30,1,[\"Content\"]],null,null,[[\"default\"],[[[[1,\"\\n    content\\n  \"]],[]]]]],[1,\"\\n\"]],[1]]]]],[1,\"\\n\\nafter basic dropdown\\n\\n\"],[46,[28,[37,1],null,null],null,null,null]],[\"dd\"],false,[\"component\",\"-outlet\"]]",
  "moduleName": "missing-helpers/templates/application.hbs",
  "scope": () => [_helpers_page_title_js__WEBPACK_IMPORTED_MODULE_3__["default"], _helpers_or_js__WEBPACK_IMPORTED_MODULE_2__["default"], _components_basic_dropdown_js__WEBPACK_IMPORTED_MODULE_1__["default"]],
  "isStrictMode": false
}));

//# sourceURL=webpack://missing-helpers/./templates/application.hbs?
```

`basic-dropdown.hbs` errors while invoking a helper, and its compiled form (`basic-dropdown.hbs.js`) is:

```js
__webpack_require__.r(__webpack_exports__);
/* harmony export */ __webpack_require__.d(__webpack_exports__, {
/* harmony export */   "default": () => (__WEBPACK_DEFAULT_EXPORT__)
/* harmony export */ });
/* harmony import */ var _externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ../../../../externals/@ember/template-factory */ "../externals/@ember/template-factory.js");
/* harmony import */ var _externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0___default = /*#__PURE__*/__webpack_require__.n(_externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0__);

/* harmony default export */ const __WEBPACK_DEFAULT_EXPORT__ = ((0,_externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_0__.createTemplateFactory)(
/*
  {{#let
  (hash
    uniqueId=this.publicAPI.uniqueId
    isOpen=this.publicAPI.isOpen
    disabled=this.publicAPI.disabled
    actions=this.publicAPI.actions
    Trigger=(if
      (eq @triggerComponent undefined)
      (component
        'basic-dropdown-trigger'
        dropdown=(readonly this.publicAPI)
        hPosition=(readonly this.hPosition)
        renderInPlace=(readonly this.renderInPlace)
        vPosition=(readonly this.vPosition)
      )
      (component
        (ensure-safe-component @triggerComponent)
        dropdown=(readonly this.publicAPI)
        hPosition=(readonly this.hPosition)
        renderInPlace=(readonly this.renderInPlace)
        vPosition=(readonly this.vPosition)
      )
    )
    Content=(if
      (eq @contentComponent undefined)
      (component
        'basic-dropdown-content'
        dropdown=(readonly this.publicAPI)
        hPosition=(readonly this.hPosition)
        renderInPlace=(readonly this.renderInPlace)
        preventScroll=(readonly @preventScroll)
        rootEventType=(or @rootEventType 'click')
        vPosition=(readonly this.vPosition)
        destination=(readonly this.destination)
        top=(readonly this.top)
        left=(readonly this.left)
        right=(readonly this.right)
        width=(readonly this.width)
        height=(readonly this.height)
        otherStyles=(readonly this.otherStyles)
      )
      (component
        (ensure-safe-component @contentComponent)
        dropdown=(readonly this.publicAPI)
        hPosition=(readonly this.hPosition)
        renderInPlace=(readonly this.renderInPlace)
        preventScroll=(readonly @preventScroll)
        rootEventType=(or @rootEventType 'click')
        vPosition=(readonly this.vPosition)
        destination=(readonly this.destination)
        top=(readonly this.top)
        left=(readonly this.left)
        right=(readonly this.right)
        width=(readonly this.width)
        height=(readonly this.height)
        otherStyles=(readonly this.otherStyles)
      )
    )
  )
as |api|
}}
  {{#if this.renderInPlace}}
    <div class='ember-basic-dropdown' ...attributes>{{yield api}}</div>
  {{else}}
    {{yield api}}
  {{/if}}
{{/let}}
*/
{
  "id": "nDnUvDqh",
  "block": "[[[44,[[28,[37,1],null,[[\"uniqueId\",\"isOpen\",\"disabled\",\"actions\",\"Trigger\",\"Content\"],[[30,0,[\"publicAPI\",\"uniqueId\"]],[30,0,[\"publicAPI\",\"isOpen\"]],[30,0,[\"publicAPI\",\"disabled\"]],[30,0,[\"publicAPI\",\"actions\"]],[52,[28,[37,3],[[30,1],[27]],null],[50,\"basic-dropdown-trigger\",0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"vPosition\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null]]]],[50,[28,[37,6],[[30,1]],null],0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"vPosition\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null]]]]],[52,[28,[37,3],[[30,2],[27]],null],[50,\"basic-dropdown-content\",0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"preventScroll\",\"rootEventType\",\"vPosition\",\"destination\",\"top\",\"left\",\"right\",\"width\",\"height\",\"otherStyles\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,3]],null],[28,[37,7],[[30,4],\"click\"],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null],[28,[37,5],[[30,0,[\"destination\"]]],null],[28,[37,5],[[30,0,[\"top\"]]],null],[28,[37,5],[[30,0,[\"left\"]]],null],[28,[37,5],[[30,0,[\"right\"]]],null],[28,[37,5],[[30,0,[\"width\"]]],null],[28,[37,5],[[30,0,[\"height\"]]],null],[28,[37,5],[[30,0,[\"otherStyles\"]]],null]]]],[50,[28,[37,6],[[30,2]],null],0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"preventScroll\",\"rootEventType\",\"vPosition\",\"destination\",\"top\",\"left\",\"right\",\"width\",\"height\",\"otherStyles\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,3]],null],[28,[37,7],[[30,4],\"click\"],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null],[28,[37,5],[[30,0,[\"destination\"]]],null],[28,[37,5],[[30,0,[\"top\"]]],null],[28,[37,5],[[30,0,[\"left\"]]],null],[28,[37,5],[[30,0,[\"right\"]]],null],[28,[37,5],[[30,0,[\"width\"]]],null],[28,[37,5],[[30,0,[\"height\"]]],null],[28,[37,5],[[30,0,[\"otherStyles\"]]],null]]]]]]]]],[[[41,[30,0,[\"renderInPlace\"]],[[[1,\"    \"],[11,0],[24,0,\"ember-basic-dropdown\"],[17,6],[12],[18,7,[[30,5]]],[13],[1,\"\\n\"]],[]],[[[1,\"    \"],[18,7,[[30,5]]],[1,\"\\n\"]],[]]]],[5]]]],[\"@triggerComponent\",\"@contentComponent\",\"@preventScroll\",\"@rootEventType\",\"api\",\"&attrs\",\"&default\"],false,[\"let\",\"hash\",\"if\",\"eq\",\"component\",\"readonly\",\"ensure-safe-component\",\"or\",\"yield\"]]",
  "moduleName": "ember-basic-dropdown/components/basic-dropdown.hbs",
  "isStrictMode": false
}));

//# sourceURL=webpack://missing-helpers/./node_modules/ember-basic-dropdown/components/basic-dropdown.hbs.js?
```

Note that `application.hbs`'s compiled template has a `scope` property that provides all the helpers it invokes, while `basic-dropdown.hbs.js` does not -- this is the closest my investigation has gotten to the root cause of the problem, and I'm hoping somebody more familiar with the template compilation pipeline will be able to easily find the root cause based on this.

In case it's helpful, there is no error under embroider 1.x, which produces a `basic-dropdown.hbs` that looks like:

```js
__webpack_require__.r(__webpack_exports__);
/* harmony export */ __webpack_require__.d(__webpack_exports__, {
/* harmony export */   "default": () => (__WEBPACK_DEFAULT_EXPORT__)
/* harmony export */ });
/* harmony import */ var _helpers_or_js__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ../../../helpers/or.js */ "./helpers/or.js");
/* harmony import */ var _components_basic_dropdown_content_js__WEBPACK_IMPORTED_MODULE_1__ = __webpack_require__(/*! ../../../components/basic-dropdown-content.js */ "./components/basic-dropdown-content.js");
/* harmony import */ var _helpers_ensure_safe_component_js__WEBPACK_IMPORTED_MODULE_2__ = __webpack_require__(/*! ../../../helpers/ensure-safe-component.js */ "./helpers/ensure-safe-component.js");
/* harmony import */ var _components_basic_dropdown_trigger_js__WEBPACK_IMPORTED_MODULE_3__ = __webpack_require__(/*! ../../../components/basic-dropdown-trigger.js */ "./components/basic-dropdown-trigger.js");
/* harmony import */ var _helpers_eq_js__WEBPACK_IMPORTED_MODULE_4__ = __webpack_require__(/*! ../../../helpers/eq.js */ "./helpers/eq.js");
/* harmony import */ var _externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_5__ = __webpack_require__(/*! ../../../../externals/@ember/template-factory */ "../externals/@ember/template-factory.js");
/* harmony import */ var _externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_5___default = /*#__PURE__*/__webpack_require__.n(_externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_5__);

window.define("missing-helpers/helpers/or", function () {
  return _helpers_or_js__WEBPACK_IMPORTED_MODULE_0__["default"];
});

window.define("missing-helpers/components/basic-dropdown-content", function () {
  return _components_basic_dropdown_content_js__WEBPACK_IMPORTED_MODULE_1__["default"];
});

window.define("missing-helpers/helpers/ensure-safe-component", function () {
  return _helpers_ensure_safe_component_js__WEBPACK_IMPORTED_MODULE_2__["default"];
});

window.define("missing-helpers/components/basic-dropdown-trigger", function () {
  return _components_basic_dropdown_trigger_js__WEBPACK_IMPORTED_MODULE_3__["default"];
});

window.define("missing-helpers/helpers/eq", function () {
  return _helpers_eq_js__WEBPACK_IMPORTED_MODULE_4__["default"];
});

/* harmony default export */ const __WEBPACK_DEFAULT_EXPORT__ = ((0,_externals_ember_template_factory__WEBPACK_IMPORTED_MODULE_5__.createTemplateFactory)(
/*
  {{#let (hash uniqueId=this.publicAPI.uniqueId isOpen=this.publicAPI.isOpen disabled=this.publicAPI.disabled actions=this.publicAPI.actions Trigger=(if (eq @triggerComponent undefined) (component "basic-dropdown-trigger" dropdown=(readonly this.publicAPI) hPosition=(readonly this.hPosition) renderInPlace=(readonly this.renderInPlace) vPosition=(readonly this.vPosition)) (component (ensure-safe-component @triggerComponent) dropdown=(readonly this.publicAPI) hPosition=(readonly this.hPosition) renderInPlace=(readonly this.renderInPlace) vPosition=(readonly this.vPosition))) Content=(if (eq @contentComponent undefined) (component "basic-dropdown-content" dropdown=(readonly this.publicAPI) hPosition=(readonly this.hPosition) renderInPlace=(readonly this.renderInPlace) preventScroll=(readonly @preventScroll) rootEventType=(or @rootEventType "click") vPosition=(readonly this.vPosition) destination=(readonly this.destination) top=(readonly this.top) left=(readonly this.left) right=(readonly this.right) width=(readonly this.width) height=(readonly this.height) otherStyles=(readonly this.otherStyles)) (component (ensure-safe-component @contentComponent) dropdown=(readonly this.publicAPI) hPosition=(readonly this.hPosition) renderInPlace=(readonly this.renderInPlace) preventScroll=(readonly @preventScroll) rootEventType=(or @rootEventType "click") vPosition=(readonly this.vPosition) destination=(readonly this.destination) top=(readonly this.top) left=(readonly this.left) right=(readonly this.right) width=(readonly this.width) height=(readonly this.height) otherStyles=(readonly this.otherStyles)))) as |api|}}
  {{#if this.renderInPlace}}
    <div class="ember-basic-dropdown" ...attributes>{{yield api}}</div>
  {{else}}
    {{yield api}}
  {{/if}}
{{/let}}
*/
{
  "id": "nDnUvDqh",
  "block": "[[[44,[[28,[37,1],null,[[\"uniqueId\",\"isOpen\",\"disabled\",\"actions\",\"Trigger\",\"Content\"],[[30,0,[\"publicAPI\",\"uniqueId\"]],[30,0,[\"publicAPI\",\"isOpen\"]],[30,0,[\"publicAPI\",\"disabled\"]],[30,0,[\"publicAPI\",\"actions\"]],[52,[28,[37,3],[[30,1],[27]],null],[50,\"basic-dropdown-trigger\",0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"vPosition\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null]]]],[50,[28,[37,6],[[30,1]],null],0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"vPosition\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null]]]]],[52,[28,[37,3],[[30,2],[27]],null],[50,\"basic-dropdown-content\",0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"preventScroll\",\"rootEventType\",\"vPosition\",\"destination\",\"top\",\"left\",\"right\",\"width\",\"height\",\"otherStyles\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,3]],null],[28,[37,7],[[30,4],\"click\"],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null],[28,[37,5],[[30,0,[\"destination\"]]],null],[28,[37,5],[[30,0,[\"top\"]]],null],[28,[37,5],[[30,0,[\"left\"]]],null],[28,[37,5],[[30,0,[\"right\"]]],null],[28,[37,5],[[30,0,[\"width\"]]],null],[28,[37,5],[[30,0,[\"height\"]]],null],[28,[37,5],[[30,0,[\"otherStyles\"]]],null]]]],[50,[28,[37,6],[[30,2]],null],0,null,[[\"dropdown\",\"hPosition\",\"renderInPlace\",\"preventScroll\",\"rootEventType\",\"vPosition\",\"destination\",\"top\",\"left\",\"right\",\"width\",\"height\",\"otherStyles\"],[[28,[37,5],[[30,0,[\"publicAPI\"]]],null],[28,[37,5],[[30,0,[\"hPosition\"]]],null],[28,[37,5],[[30,0,[\"renderInPlace\"]]],null],[28,[37,5],[[30,3]],null],[28,[37,7],[[30,4],\"click\"],null],[28,[37,5],[[30,0,[\"vPosition\"]]],null],[28,[37,5],[[30,0,[\"destination\"]]],null],[28,[37,5],[[30,0,[\"top\"]]],null],[28,[37,5],[[30,0,[\"left\"]]],null],[28,[37,5],[[30,0,[\"right\"]]],null],[28,[37,5],[[30,0,[\"width\"]]],null],[28,[37,5],[[30,0,[\"height\"]]],null],[28,[37,5],[[30,0,[\"otherStyles\"]]],null]]]]]]]]],[[[41,[30,0,[\"renderInPlace\"]],[[[1,\"    \"],[11,0],[24,0,\"ember-basic-dropdown\"],[17,6],[12],[18,7,[[30,5]]],[13],[1,\"\\n\"]],[]],[[[1,\"    \"],[18,7,[[30,5]]],[1,\"\\n\"]],[]]]],[5]]]],[\"@triggerComponent\",\"@contentComponent\",\"@preventScroll\",\"@rootEventType\",\"api\",\"&attrs\",\"&default\"],false,[\"let\",\"hash\",\"if\",\"eq\",\"component\",\"readonly\",\"ensure-safe-component\",\"or\",\"yield\"]]",
  "moduleName": "ember-basic-dropdown/components/basic-dropdown.hbs",
  "isStrictMode": false
}));

//# sourceURL=webpack://missing-helpers/./node_modules/ember-basic-dropdown/components/basic-dropdown.hbs?
```