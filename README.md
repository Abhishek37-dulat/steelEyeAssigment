1.Explain what the simple List component does. 

 

=> 

List component are used to represent data in particular order as they are easy to maintain. 

In this code we are using 'map’ to extract each item from list of  items. 

 

2. What problems / warnings are there with code? 

 

=> 
![err1](https://user-images.githubusercontent.com/63417558/193464156-b5d08aae-5fd0-41ee-b95d-b743391dd07a.PNG)
 ![err2](https://user-images.githubusercontent.com/63417558/193464203-3d2e288d-a2ea-4121-a130-9f62a6bb6961.PNG)
![err3](https://user-images.githubusercontent.com/63417558/193464236-baa6b359-66bd-437d-b0d3-729365faf61f.PNG)
![err4](https://user-images.githubusercontent.com/63417558/193464240-c5a606c9-3668-4f08-bbe7-aa5570bba561.PNG)
![err5](https://user-images.githubusercontent.com/63417558/193464243-0047738b-2a59-400b-baab-36ef8d44e973.PNG)
![err6](https://user-images.githubusercontent.com/63417558/193464246-ddd3a577-26c9-4dd6-a81d-8990c67e38b1.PNG)
![err7](https://user-images.githubusercontent.com/63417558/193464247-b946fdf6-16de-469e-af53-e8401e348938.PNG)
![err8](https://user-images.githubusercontent.com/63417558/193464249-85b2e4fb-73ab-4599-b82a-0e0a046c3ff0.PNG)
![err9](https://user-images.githubusercontent.com/63417558/193464254-119e74ce-3a44-4a19-b49b-ff96f7dfa17c.PNG)
![codeerr1](https://user-images.githubusercontent.com/63417558/193464269-8fa68589-2e1e-4532-978f-348b498ed5d5.PNG)
![codeerr2](https://user-images.githubusercontent.com/63417558/193464271-86f38900-db3b-4bb9-b014-701fa6f4335c.PNG)
![codeerr3](https://user-images.githubusercontent.com/63417558/193464273-121d93f8-c222-4c80-8ea4-9bd660ba5bc2.PNG)
![codeerr4](https://user-images.githubusercontent.com/63417558/193464274-bd8e82cc-556d-42c4-a5e3-be6bcafac68b.PNG)
![codeerr5](https://user-images.githubusercontent.com/63417558/193464276-01dc88c8-8b04-480f-bdcf-49ad9cb0e648.PNG)
![codeerr6](https://user-images.githubusercontent.com/63417558/193464278-08b6ca93-000b-49da-9ced-4929e89aa8ab.PNG)

 

3. Please fix, optimize, and/or modify the component as much as you think is necessary. 

 

=> errors: 

  

1.array -> arrayOf 

2.shapeOf -> shape 

3.items -> cann't be null 

4.onClickHandler={()=>handleClick(index)} -> onClickHandler={handleClick} 

5.key={index} should be there 

6.setSelectedIndex(null) -> setSelectedIndex(false)  

7.onClick={onClickHandler(index)} -> onClick={()=>onClickHandler(!isSelected)} 

8.{index} 

 

Optimized code=> 

import React, { useState, useEffect, memo } from 'react'; 

import PropTypes from 'prop-types'; 

 
 

// Single List Item 

const WrappedSingleListItem = ({ 

  index, 

  isSelected, 

  onClickHandler, 

  text, 

}) => { 

  return ( 

    <li 

      style={{ backgroundColor: isSelected ? 'green' : 'red'}} 

      onClick={()=>onClickHandler(!isSelected)} 

    > 

      {index} {text} 

    </li> 

  ); 

}; 

 
 

WrappedSingleListItem.propTypes = { 

  index: PropTypes.number, 

  isSelected: PropTypes.bool, 

  onClickHandler: PropTypes.func.isRequired, 

  text: PropTypes.string.isRequired, 

}; 

 
 

const SingleListItem = memo(WrappedSingleListItem); 

 
 

// List Component 

const WrappedListComponent = ({ 

  items, 

}) => { 

  console.log(items) 

  const [selectedIndex, setSelectedIndex] = useState(); 

 
 

  useEffect(() => { 

    setSelectedIndex(false); 

  }, [items]); 

 
 

  const handleClick = (index) => { 

    setSelectedIndex(index); 

  }; 

 
 

  return ( 

    <ul style={{ textAlign: 'left' }}> 

      {items.map((item, index) => ( 

        <SingleListItem 

          key={index} 

          onClickHandler={handleClick} 

          text={item.text} 

          index={index} 

          isSelected={selectedIndex} 

        /> 

      ))} 

    </ul> 

  ) 

}; 


WrappedListComponent.propTypes = { 

  items: PropTypes.arrayOf(PropTypes.shape({ 

    text: PropTypes.string.isRequired, 

  })), 

}; 

WrappedListComponent.defaultProps = { 
  items: [{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'},{text:'h1'}], 
}; 


const List = memo(WrappedListComponent); 

export default List; 
