# 二次开发

## render props

组件尽量提供 `render props` 便于二次开发,
# 二次开发

## render props

组件尽量提供 `render props` 便于二次开发,

### $render

```js
<Button
	prepend="&copy;"
	render={function(own){
		return (
			<span
				{...own.$render('rootProps')}
			>
			{own.$render('renderPrepend')}
			{own.props.children}
			{own.$render('renderAppend')}
			</span>
		)
	}}
>abc</Button>
```

### $emit


```js
<Trigger
	popup={function(own){
		return (
			<div>
			1
			2
			3
			<button onClick={function(){
				own.$emit('hide')
			}} >hide</button>
			</div>
		)
	}}
>
click
</Trigger>
```

`render`接口中，统一将`own`作为第一个参数，可以调用 `own.$emit` `own.$render` 和查询 `own.props` `own.state` ,但是不要调用`own.setState`

如果要修改内部状态，说明是要对功能进行二次封装。



例如:


### 点击获取文字
```js
<Button
	$fetch="https://echo.onface.live/onface/echo/mock/poem"
>
点击
</Button>
```

### 封装代码

```js
class CustonButton extend compents {
	constructor(props){
		super(props)
		this.state = {
			busy: false,
			text: ''
		}
	}
	fetch = () => {
		let self = this
		self.setState({
			busy: true
		})
		$.ajax({
			type: 'get',
			url: self.props.$fetch
		}).done(function(res){
			self.setState({
				text: res
			})
		}).always(function () {
			self.setState({
				busy: false
			})	
		})
	}
	render(){
		const self = this
		let iconType
		if (self.state.busy) {
			iconType = 'loading'
		}
		else {
			iconType = 'reload'
		}
		return (
			<Button
				append={(
					<Icon 
						type={iconType}
						onClick={function(){
							self.fetch()
						}}
					/>
				)}
			>
				{
					self.state.text?
					self.state.text:
					self.props.children
				}
			</Button>
		)
	}
}
```

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

`render`接口中，统一将`self`作为第一个参数，可以调用 `self.$emit` `self.$render` 和查询 `self.props` `self.state` ,但是不要调用`self.setState`

如果要修改内部状态，说明是要对功能进行二次封装。



例如:


### 点击获取文字
```js
<Button
	$fetch="https://echo.onface.live/onface/echo/mock/poem"
>
点击
</Button>
```

### 封装代码

```js
class CustonButton extend compents {
	constructor(props){
		super(props)
		this.state = {
			busy: false,
			text: ''
		}
	}
	fetch = () => {
		let self = this
		self.setState({
			busy: true
		})
		$.ajax({
			type: 'get',
			url: self.props.$fetch
		}).done(function(res){
			self.setState({
				text: res
			})
		}).always(function () {
			self.setState({
				busy: false
			})	
		})
	}
	render(){
		const self = this
		let iconType
		if (self.state.busy) {
			iconType = 'loading'
		}
		else {
			iconType = 'reload'
		}
		return (
			<Button
				append={(
					<Icon 
						type={iconType}
						onClick={function(){
							self.fetch()
						}}
					/>
				)}
			>
				{
					self.state.text?
					self.state.text:
					self.props.children
				}
			</Button>
		)
	}
}
```
