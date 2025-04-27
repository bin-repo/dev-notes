# CSS 示例

## justify-content

```html
<div class="container">
    <div class="box a">1</div>
    <div class="box b">2</div>
    <div class="box c">3</div>
</div>
```

```css
.container {
    border: 1px solid grey;
    display: flex;
    justify-content: flex-start;
    justify-content: flex-end;
    justify-content: center;
    justify-content: space-between;
    justify-content: space-around;
    justify-content: space-evenly; 
}
.box {
    width:30px;
    height:30px;
    padding:5px;
    margin: 10px;
    border:1px solid grey;
    text-align: center;
    line-height: 30px;
    border-radius: 5px;
}
```
