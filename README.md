# 前言

`

花了3天时间去看了一下Field-form,整理了一份自己的源码见解,如果有讲的不好的地方，轻骂

代码选择性讲解
`
![006tuqRIly1gf3mr4dcmij30jf0ijdhv](_v_images/20200524233545307_11189.jpg =400x)

## Field-form

React Performance First Form Component.

* github地址:[field-form](https://github.com/react-component/field-form)

* Field-form是antd v4.0的Form组件的底层组件

## 整体的逻辑架构

![BV1rD4y1D7Kb?spm_id_from=333](./TIM图片20200603031944.png)

大体逻辑如上

```markdown
 <Form>
          <Field name="username">
            <Input placeholder="Username" />
          </Field>
          <Field name="password">
            <Input placeholder="Password" />
          </Field>
          <Field name="username">
            <Input placeholder="Shadow of Username" />
          </Field>
          <Field name={['path1', 'path2']}>
            <Input placeholder="nest" />
          </Field>
</Form>

```

上面是一段很基本的代码....我们就从`example`入手,Field会在组件挂载完成的时候注册到Form中，Form会获得每个Field的实例,当操作Field.Children下的组件的时候

会通过dispatch通知Form---------------Field.Children会在渲染的时候会被劫持掉onChange(这个是通过trigger来指定的，默认是onChange)

Form就会调用每个Field的onStoreChange来对Field进行操作.

### dispatch的action.type分别是两种

* type===updateValue
