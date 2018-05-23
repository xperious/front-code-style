# TripCreator front code style

  - [1.](#order-in-files) **Order in files**:

    - imports
    - interfaces
    - constants
    - styled components
    - react component


  - [2.](#uppercase-constants) **Use upper case for constants **:

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

  - [3.](#name-variables-to-connect) **Always pass named variables mapStateToProps and mapDispatchToProps to connect() method**:

    ```javascript
    // bad
    export const AccommodationGroups = connect(
      ({ accommodationGroups }: RootState): OwnProps => ({
        groups: accommodationGroups.groups,
      }),
      (dispatch: Dispatch<m.Actions>) => ({
        actions: bindActionCreators(accommodationGroupsActions, dispatch)
      }))(Component);

    // good
    const mapStateToProps = ({ accommodationGroups }: RootState): OwnProps => ({
      groups: accommodationGroups.groups,
    });

    const mapDispatchToProps = (dispatch: Dispatch<m.Actions>) => ({
      actions: bindActionCreators(accommodationGroupsActions, dispatch)
    });

    export const AccommodationGroups = connect(mapStateToProps, mapDispatchToProps)(Component);

    ```

  - [4.](#use-bind-action-creators) **Always use bindActionCreators, do not use this.props.dispatch**:

    ```javascript
    // bad
    const mapDispatchToProps = (dispatch: Dispatch<m.Actions>) => ({
      dispatch
    });

    ...

    this.props.dispatch(accommodationGroupsActions.loadGroups());

    // good
    const mapDispatchToProps = (dispatch: Dispatch<m.Actions>) => ({
      actions: bindActionCreators(accommodationGroupsActions, dispatch)
    });

    ...

    const { actions } = this.props;
    actions.loadGroups();

    ```

  - [5.](#curly-brackets-space) **Add spaces between curly brackets and object properties**:

    ```javascript
    // bad
    const {actions} = this.props;

    // good
    const { actions } = this.props;

    ```

  - [6.](#do-not-use-bind) **Do not use method.bind(this) or method = () => {}  when () => method() is possible to use**:

    ```javascript
    // bad
    <Link onClick={ this.toggle.bind(this) }>Select</Link>


    // good
    <Link onClick={ () => this.toggle() }>Select</Link>

    ```

  - [7.](#do-not-use-default-exports) **Do not use default exports**:

    ```javascript
    // bad
    class Textarea extends React.Component<{}> {}
    export default Textarea;

    // good
    export class Textarea extends React.Component<{}> {}

    ```

  - [7.](#uncscoped-naming-for-exported-variables) **Do not use unscoped naming for exported variables**:

    ```javascript
    // bad
    export const reducer = ...

    // good
    export const cartInfoReducer = ...

    ```

  - [8.](#common-naming-for-private-variables) **For private variables, use common naming**:

    ```javascript
    // bad
    const TimePickerContainer => styled.div``;

    interface TimePickerProps {}

    // good
    const Container => styled.div``;

    interface Props {}

    ```

  - [9.](#define-method-return type) **Always define method return type, unless it is void**:

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

  - [10.](#atributes-in-separate-lines) **When element has multiple attributes, write them in separate lines, as well as closing tag**:

    ```javascript
    // bad
    <ItineraryItemHeader
      inventorized={ true }
      address={ locationTitle } />

    // good
    <ItineraryItemHeader
      inventorized={ true }
      address={ locationTitle }
    />

    ```

  - [11.](#action-names) **For action names, use structure app/feature/action**:

    ```javascript
    // bad
    const LOAD_CAR_ALTERNATIVES = 'LOAD_CAR_ALTERNATIVES';

    // good
    const CAR_ALTERNATIVES_LOAD = 'checkout/CAR/ALTERNATIVES/LOAD';

    ```

  - [12.](#action-names) **Use same indentation everywhere**:

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
