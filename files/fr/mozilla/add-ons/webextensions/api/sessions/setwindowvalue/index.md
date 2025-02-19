---
title: sessions.setWindowValue()
slug: Mozilla/Add-ons/WebExtensions/API/sessions/setWindowValue
translation_of: Mozilla/Add-ons/WebExtensions/API/sessions/setWindowValue
---

{{AddonSidebar()}}

Stocke une paire clé / valeur à associer à une fenêtre donnée. Vous pouvez ensuite récupérer cette valeur en utilisant {{WebExtAPIRef("sessions.getWindowValue")}}.

Notez que ces données ne seront visibles que par l'extension qui l'a définie, et non par les autres extensions..

C'est une fonction asynchrone qui renvoie une [`Promise`](/fr/docs/Web/JavaScript/Reference/Objets_globaux/Promise).

## Syntaxe

```js
var storing = browser.sessions.setWindowValue(
  windowId,    // integer
  key,         // string
  value        // string or object
)
```

### Paramètres

- `windowId`
  - : `integer`. ID de la fenêtre avec laquelle vous souhaitez associer les données.
- `key`
  - : `string`. Clé que vous pouvez utiliser ultérieurement pour récupérer cette valeur de données particulière.
- `value`
  - : `string` ou `object`. S'il s'agit d'un objet, il est [stringified](/fr/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), donc les méthodes d'objet, par exemple, seront omises. Si une fonction est donnée ici, elle sera stockée sous la valeur `null`.

### Valeur retournée

Une [`Promise`](/fr/docs/Web/JavaScript/Reference/Objets_globaux/Promise) qui sera résolue sans argument si l'appel a réussi. Si l'appel a échoué (par exemple, parce que l'ID de la fenêtre n'a pas pu être trouvé), la promesse sera rejetée avec un message d'erreur.

## Compatibilité des navigateurs

{{Compat}}

## Exemples

Définissez une valeur sur la fenêtre active lorsque l'utilisateur sélectionne un élément de menu. Notez que vous aurez besoin de la [permission](/fr/Add-ons/WebExtensions/manifest.json/permissions) "menus" pour exécuter cet exemple :

```js
async function setOnActiveWindow() {
  let currentWindow = await browser.windows.getLastFocused();
  await browser.sessions.setWindowValue(currentWindow.id, "my-key", "my-value");
}

browser.menus.create({
  id: "my-item",
  title: "my item",
  contexts: ["all"]
});

browser.menus.onClicked.addListener(setOnActiveWindow);
```

{{WebExtExamples}}
