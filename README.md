# Challenge 1

## SOLUTION

### Singleton Design Pattern
This code segment demonstrates the use of the **Singleton design pattern** with a PHP class, `DataBaseConnector`. The Singleton pattern ensures that a class has only one instance and provides a global point of access to it.

### Implementation Details

- **Private Constructor**: The constructor of the `DataBaseConnector` class is private to prevent the instantiation of the class from outside.
- **Static Instance Variable**: A private static variable `$obj` holds the instance of the class.
- **Public Static Method**: The `getConnect()` static method checks if the class instance exists and returns it if available. If not, it creates a new instance, stores it in the static variable, and then returns it.

### Usage

Here is how you can use the `DataBaseConnector` class to ensure that only one instance of the database connection is used across your application:

```php
// Getting the instance of DataBaseConnector
$obj1 = DataBaseConnector::getConnect();
$obj2 = DataBaseConnector::getConnect();

// Checking if both instances are the same
var_dump($obj1 == $obj2);  // Outputs: bool(true)
```

# Challenge 2

## SOLUTION

```sql
SELECT
    c.customer_id AS CUSTOMER_ID,
    c.firstname AS FIRSTNAME,
    c.lastname AS LASTNAME,
    CAST(AVG(p.product_count) AS DECIMAL(10, 2)) AS AVG
FROM
    customer c
JOIN purchase_order po ON
    c.customer_id = po.customer_id
JOIN(
    SELECT
        order_id,
        COUNT(product_id) AS product_count
    FROM
        order_product
    GROUP BY
        order_id
) p
ON
    po.order_id = p.order_id
GROUP BY
    c.customer_id
HAVING
    AVG(p.product_count) > 2
ORDER BY
    AVG(p.product_count)
DESC
```

# Challenge 3

## SOLUTION
```php
<?php

/**
 * Class TemperatureStats provides methods to analyze temperature data.
 */
class TemperatureStats {
    /**
     * Finds the temperature closest to zero from an array of temperatures.
     * This method assumes that temperatures are always within the range of -273 to 5526.
     *
     * @param array $temperatures Array of floating point numbers representing temperatures.
     * @return float Returns the temperature closest to zero, or 0 if the array is empty.
     */
    public function closestToZero(array $temperatures): float
    {
        // Return 0 if the array is empty
        if (empty($temperatures)) {
            return 0.0;
        }

        // Initialize the closest temperature to the first element in the array
        $closest = $temperatures[0];

        // Loop through the temperatures to find the one closest to zero
        foreach ($temperatures as $temperature) {
            // Check if the current temperature is closer to zero than the previously found closest
            if (abs($temperature) < abs($closest)) {
                $closest = $temperature;
            } elseif (abs($temperature) === abs($closest)) {
                // If two temperatures are equally close to zero, prefer the positive one
                if ($temperature > $closest) {
                    $closest = $temperature;
                }
            }
        }

        return $closest;
    }
}

// Example usage
$analyzer = new TemperatureStats();
$temperatures = [7, -10, 13, 8, 4, -7.2, -12, -3.7, 3.5, -9.6, 6.5, -1.7, -6.2, 7];
echo $analyzer->closestToZero($temperatures);  // Outputs: -1.7

?>
```