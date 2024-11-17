# DELETE-API-INTEGRATION

```javascript
import React, { useState, useEffect } from "react";

function DeleteItem() {
  const [items, setItems] = useState([]);

  // Simulating API data fetch
  useEffect(() => {
    // Fetch initial data from API
    const fetchItems = async () => {
      const response = await fetch("https://api.example.com/items");
      const data = await response.json();
      setItems(data);
    };
    fetchItems();
  }, []);

  const handleDelete = async (id) => {
    try {
      const response = await fetch(`https://api.example.com/items/${id}`, {
        method: "DELETE",
      });

      if (response.ok) {
        console.log(`Item with ID ${id} deleted successfully!`);
        // Update items state
        setItems((prevItems) =>
          prevItems.filter((item) => item.id !== id)
        );
      } else {
        console.error("Failed to delete the item.");
      }
    } catch (error) {
      console.error("Error deleting item:", error);
    }
  };

  return (
    <div>
      <h2>Item List</h2>
      {items.length > 0 ? (
        <ul>
          {items.map((item) => (
            <li key={item.id}>
              {item.name}{" "}
              <button onClick={() => handleDelete(item.id)}>Delete</button>
            </li>
          ))}
        </ul>
      ) : (
        <p>No items found.</p>
      )}
    </div>
  );
}

export default DeleteItem;
```







