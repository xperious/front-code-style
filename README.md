# TripCreator front code style


<a name="order-in-files"></a>
[1.](#order-in-files) **Order in files**:

  - imports
  - constants
  - styled components
  - react component

  Define interfaces above components that use them

<a name="uppercase-constants"></a>
[2.](#uppercase-constants) **Use upper case for constants**:

  ```javascript
  // bad
  const buttonHeight = 30;

  const footerConstants = {
    height: 50,
    ...
  }

  // good
  const BUTTON_HEIGHT = 30;

  const FOOTER_CONSTANTS = {
    height: 50
    ...
  }

  ```

<a name="named-variables-to-connect"></a>
[3.](#named-variables-to-connect) **Always pass named variables mapStateToProps and mapDispatchToProps to connect() method**:

  ```javascript
  // bad
  export const AccommodationGroups = connect(
    ({ accommodationGroups }: RootState): OwnProps => ({
      groups: accommodationGroups.groups,
    }),
    (dispatch: Dispatch<m.Actions>) => ({
      dispatch
    }))(Component);

  // good
  const mapStateToProps = ({ accommodationGroups }: RootState): OwnProps => ({
    groups: accommodationGroups.groups,
  });

  const mapDispatchToProps = (dispatch: Dispatch<m.Actions>) => ({
    dispatch
  });

  export const AccommodationGroups = connect(mapStateToProps, mapDispatchToProps)(Component);

  ```

<a name="use-bind-action-creators"></a>
[4.](#use-bind-action-creators) **Use dispatch instead of bindActionCreators**:

  ```javascript
  // bad
  const mapDispatchToProps = (dispatch: Dispatch<m.Actions>) => ({
    actions: bindActionCreators(accommodationGroupsActions, dispatch)
  });

  ...

  const { actions } = this.props;
  actions.loadGroups();

  // good
  const mapDispatchToProps = (dispatch: Dispatch<m.Actions>) => ({
    dispatch
  });

  ...

  this.props.dispatch(accommodationGroupsActions.loadGroups());

  ```

<a name="curly-brackets-space"></a>
[5.](#curly-brackets-space) **Add spaces between curly brackets and object properties**:

  ```javascript
  // bad
  const {actions} = this.props;

  // good
  const { actions } = this.props;

  ```

<a name="do-not-use-bind"></a>
[6.](#do-not-use-bind) **Do not use method.bind(this) or method = () => {}  when () => method() is possible to use**:

  ```javascript
  // bad
  <Link onClick={ this.toggle.bind(this) }>Select</Link>


  // good
  <Link onClick={ () => this.toggle() }>Select</Link>

  ```

<a name="do-not-use-default-exports"></a>
[7.](#do-not-use-default-exports) **Do not use default exports**:

  ```javascript
  // bad
  class Textarea extends React.Component<{}> {}
  export default Textarea;

  // good
  export class Textarea extends React.Component<{}> {}

  ```

<a name="uncscoped-naming-for-exported-variables"></a>
[8.](#uncscoped-naming-for-exported-variables) **Do not use unscoped naming for exported variables**:

  ```javascript
  // bad
  export const reducer = ...
  export type Action = GetActionTypes<typeof actions>;

  // good
  export const cartInfoReducer = ...
  export type CartInfoAction = GetActionTypes<typeof actions>;

  ```

<a name="common-naming-for-private-variables"></a>
[9.](#common-naming-for-private-variables) **For private variables, use common naming**:

  ```javascript
  // bad
  const TimePickerContainer => styled.div``;

  interface TimePickerProps {}

  // good
  const Container => styled.div``;

  interface Props {}

  ```

<a name="define-method-return-type"></a>
[10.](#define-method-return-type) **Define method return type for complex methods or which return other method**:

  ```javascript
  // bad
  export const displayDateTime = (time) => {
    return moment.utc(time).format('MMM DD, YYYY, HH:mm');
  };

  // good
  export const displayDateTime = (time): string => {
    return moment.utc(time).format('MMM DD, YYYY, HH:mm');
  };

  ```

<a name="render-prefix"></a>
[11.](#render-prefix) **Methods names, that return JSX.Elements, should start with "render"**:

  ```javascript
  // bad
  bookingNo() {
    return (
      <BookingNo>
        Number
      </BookingNo>
    );
  }

  // good
  renderBookingNo() {
    return (
      <BookingNo>
        Number
      </BookingNo>
    );
  }

  ```

<a name="atributes-in-separate-lines"></a>
[12.](#atributes-in-separate-lines) **If element's opening tag has more than one attribute, write them in separate lines, as well as closing tag (both for elements with children and without). If element has only one attribute, write it in single line**:

  ```javascript
  // bad
  <Group
    inventorized={ true }
    address={ locationTitle }>
    Group name
  </Group>

  <Group
    inventorized={ true }
    address={ locationTitle } />

  // good
  <Group
    inventorized={ true }
    address={ locationTitle }
  />

  <Group
    inventorized={ true }
    address={ locationTitle }
  >
    Group name
  </Group>

  <Group inventorized={ true }>Group name</Group>

  ```

<a name="same-indentation"></a>
[13.](#same-indentation) **Use same indentation everywhere**:

  ```javascript
  // bad
  return failingItems
          .map(i => `'${i}'`)
          .filter((v, i, a) => a.indexOf(v) === i)
          .join(', ') || fallback;

  // good
  return failingItems
    .map(i => `'${i}'`)
    .filter((v, i, a) => a.indexOf(v) === i)
    .join(', ') || fallback;

  ```
