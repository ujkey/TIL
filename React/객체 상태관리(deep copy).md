## React에서 객체 상태관리 Deep Copy 방식

<br/>

```` jsx
const [ state, setState ] = useState({
    name: 'Foo',
    address: 'Bar',
    favoriteFoods: ['candy', 'kimchi', 'bulgogi'],
    family: {
        father: { name: 'A' },
        mother: { name: 'B' },
        sister: { name: 'C' }
    }
});

function updateMotherName() {
    const newState = structuredClone(state);
    newState.family.mother.name = 'D';
    setState(newState);
}