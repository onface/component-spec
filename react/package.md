# 二次开发

## render props

组件尽量提供 `render props` 便于二次开发


### $render

```js
<Button
	prepend="&copy;"
	render={function(self){
		return (
			<span
				{...self.$render('rootProps')}
			>
			{self.$render('renderPrepend')}
			{self.props.children}
			{self.$render('renderAppend')}
			</span>
		)
	}}
>abc</Button>
```

### $emit


```js
<Trigger
	popup={function(self){
		return (
			<div>
			1
			2
			3
			<button onClick={function(){
				self.$emit('hide')
			}} >hide</button>
			</div>
		)
	}}
>
click
</Trigger>
```

