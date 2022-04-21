# DigitalTolk Code Test [Refactor]

## What I like about the codes
1. The use of Repository pattern. It’s helpful for larger systems with reuse codes.
2. Using the BookingRepository by injecting it as a dependency on BookingController. This way, it would be easier to access without constantly instantiating it.
3. Proper documentation of functions.
4. Very readable variable and function naming.


## What I think can be improved
1. There are a lot of _if…else_ whose purpose is to only assign values to variables. I prefer using **ternary operator** if it’s just a simple variable assignment as it’s easier to read and cleaner.
2. There are some conditional statements way below the functions that could result to returning values and therefore terminating the function. I prefer to put them higher up inside the function so that we don’t have to execute actions (variable assignments, other conditions, function calls, etc.) that would become useless if the said condition is satisfied.
3. Excess empty lines after opening braces ({) and/or before closing braces (}) of functions.
4. If there several chained functions, I prefer to put each on their own new line instead of in one line altogether as it presents a better glimpse of the code.
5. For no bracket _if..else_ statements, I prefer to include a black new line for new statements to avoid confusion and better readability. Such as:

```
if ($consumer_type == 'rwsconsumer')
    $data['job_type'] = 'rws';
else if ($consumer_type == 'ngo')
    $data['job_type'] = 'unpaid';
else if ($consumer_type == 'paid')
    $data['job_type'] = 'paid';
$data['b_created_at'] = date('Y-m-d H:i:s');
if (isset($due))
    $data['will_expire_at'] = TeHelper::willExpireAt($due, $data['b_created_at']);
$data['by_admin'] = isset($data['by_admin']) ? $data['by_admin'] : 'no';
```

Refactor to:
```
if ($consumer_type == 'rwsconsumer')
    $data['job_type'] = 'rws';
else if ($consumer_type == 'ngo')
    $data['job_type'] = 'unpaid';
else if ($consumer_type == 'paid')
    $data['job_type'] = 'paid';

$data['b_created_at'] = date('Y-m-d H:i:s');

if (isset($due))
    $data['will_expire_at'] = TeHelper::willExpireAt($due, $data['b_created_at']);

$data['by_admin'] = isset($data['by_admin']) ? $data['by_admin'] : 'no';
```

6. Error supressor **(@)** is really not recommended as it can be difficult to debug errors caused by expressions using this. If it's purely for determining whether the variable is required, it's better to use a validator. Other than that, try to find a better solution to handle the error.
7. It's just a minor observation, but there's an inconsistency on using the keywords _else if_ and _elseif_.