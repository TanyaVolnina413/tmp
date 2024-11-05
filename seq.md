

 1. Перетащить абилку (атаку/заклинание) в меню макросов (снизу слева)
 2. Правой кнопкой - "изменить макрос".
 Изначально там должно быть что-то вроде `"dnd5e.documents.macro.rollItem("Длинный лук /
    Longbow")"`
 3. Дописать к этому красивостей
 4. Сохранить/запустить макрос

Туториалы по красивостям:
https://fantasycomputer.works/FoundryVTT-Sequencer/#/

Но чтобы не копаться:
- Сами эффекты в "базе данных Sequencer" слева сбоку, выбрать нужный, кликнуть на значок с блинчиками, чтобы скопировать название.
- Перманентный эффекты выключать в "Менеджер Sequencer" слева сбоку

1. Сыграть быстрый эффект на свой токен:
```
new Sequence()
    .effect()
        .file("jb2a.extras.tmfx.border.circle.simple.04")
        .atLocation(token)
    .play()
```

2. Перманентный эффект на свой токен:
```
new Sequence()
    .effect()
        .file("jb2a.extras.tmfx.border.circle.simple.04")
        .attachTo(token)
        .persist()
    .play()
```
3. Быстрый эффект на токен, выбранный в качестве цели (слева сбоку, "инструменты токенов" -> мишень):
```
new Sequence()
        .effect()
            .file("jb2a.healing_generic.200px.yellow")
            .atLocation(game.user.targets.first())
        .play();
```
(Перманентный, соответственно, `.attachTo(game.user.targets.first()).persist())`

4. Выстрелить в токен-цель:
```
new Sequence()
    .effect()
        .file("jb2a.arrow.poison")
        .atLocation(token)
        .stretchTo(game.user.targets.first())
    .play()
```
5. Выбрать точку на карте и сделать что-то в неё:
```
let position = await Sequencer.Crosshair.show({
    size: 1,
    gridHighlight: false,
    label: {
        text: "SMITE",
    }
}, { show: async (crosshair) => {
    new Sequence()
        .effect().attachTo(crosshair).persist()
        .play();

}})

new Sequence()
    .effect()
    .file("jb2a.divine_smite.target")
    .atLocation(position)
.play();
```
