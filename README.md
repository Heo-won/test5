
### 1.추가하기 버튼을 클릭해도 추가한 아이템이 화면에 표시되지 않음. 
### Form.jsx에서“onSubmitHandler” 함수 내부 구현 로직에 dispatch 함수가 빠져있습니다. 
### dispatch" 함수를 사용하여 새로운 "todo" 객체와 함께 "addTodo" 액션을 발생시켜야 리듀서 함수를 통해 todos 목록이 최신 상태로 업데이트되고 변경 사항에 따라 UI가 업데이트됩니다.

### 2.추가하기 버튼 클릭 후 기존에 존재하던 아이템들이 사라짐.
### 리듀서 함수에서 todos 배열에 새로운 todo를 추가할때 기존 요소들을 모두 유지하면서 새로운 할 일을 추가해야 하기 때문에, "todos" 배열을 전개 연산자(...)로 펼쳐서 이전 요소들을 새로운 배열에 복사한 후, "action.payload"라는 새로운 할 일 객체를 마지막에 추가하는 방식을 사용했어야 합니다. 
### 이렇게 하면 이전 todos 목록을 유지하면서 새로운 todo를 추가할 수 있으며, 불변성을 유지하여 예측 가능한 상태 업데이트를 보장합니다.

### 3.삭제 기능이 동작하지 않음. 
### "DELETE_TODO"라는 타입의 액션이 디스패치될 때, "todos" 배열에서 특정 id를 가진 할 일을 삭제하는 리듀서가 빠져있었습니다.
### "filter" 함수를 사용하여 "todos" 배열에서 특정 id를 가진 todo를 제외한 새로운 배열을 만들어 리턴했습니다.

### 4.상세 페이지에 진입 하였을 때 데이터가 업데이트 되지 않음.
### useParams() 훅을 통해 URL에서 가져온 id 파라미터를 getTodoByID() 에 전달하여 useSelector()로 구독중인 todo 상태를 업데이트 해줘야 합니다.
### useEffect() 훅을 사용하여 컴포넌트가 마운트될 때 getTodoByID() 액션을 디스패치합니다.

### 5.완료된 카드의 상세 페이지에 진입 하였을 때 올바른 데이터를 불러오지 못함. 
### Detail 페이지로 이동할때 
### <StLink to={/${index}} key={todo.id}>
### url 파라미터 값으로 index가 아닌, todo.id를 전달해야 했습니다.
### <StLink to={/${todo.id}} key={todo.id}>

### 6.취소 버튼 클릭시 기능이 작동하지 않음.
### onClick={onToggleStatusTodo}
 ### 는 onToggleStatusTodo
### 함수 자체를 이벤트 핸들러로 사용하는 것입니다. 이 경우, onToggleStatusTodo
### 함수에 전달되는 id가 없다. 
### onToggleStatusTodo() 함수에 id를 전달하기 위해서는 onClick={() => onToggleStatusTodo(todo.id))}와 새로운 함수를 만들어 전달해줘야 한다.
