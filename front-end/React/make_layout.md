# 컴포넌트안에 컴포넌트 넣기

- layout.jsx
```javascript
const Layout = ({ children }) => {
  return (
    <div className={styles.layout}>
      <Header />
      <hr style={{ width: "90%", margin: "40px" }} />
      <main>{children}</main>
    </div>
  );
};
```
layout컴포넌트에 매개변수로 `children`을 넘겨준다.   
`children`을 return안에 Header나 Footer처럼 넣어준다.

- app.jsx
```javascript
    <Layout>
      <Form
        toDoTitle={toDoTitle}
        toDoComment={toDoComment}
        titleChange={titleChange}
        commentChange={commentChange}
        addToDo={addToDo}
      />
      <MyList toDoList={toDoList} done={done} remove={remove} />
    </Layout>
```
위의 형식처럼 <Layout> </Layout> 안에다가 컴포넌트를 넣으면 된다.
