<b><u><span style="font-size:1.5em;">Style</span></u></b>
1) Naming style:
~~~php
ClassName {
	functionName() {
		$variable_name
		for($count_item = 0; $count_item < $item_value; count_item++) {
		}
	}
	$arr_name = [];
}
4 space indentation.
//avoid naming variables like this
$i = 29;
//give context in the name itself like this
$user_age = 29;
~~~
2) Avoid using too many shorthands functions. This is still acceptable.
~~~php
$arr_item = [
	$item_state    => !empty($item) ? true : false,
	$item_location => $data["location"];
]
~~~
3) Avoid deep indentation. You can reduce indentation by using early exit. Take this function for example:
~~~php
function isUserRole($id) {
	$utilModel = new utilFunction();
	$valid = $utilModel->checkUserExist($id);
	if($valid) {
		$userModel = new userModel();
		$user_role = $userModel->userRole($id);
		if($user_role == "admin") {
			return true;
		}
		else {
			$data["error"] = "Unable to access this page, please try again.";
			return redirect()->view("login.php", $data);
		}
	}
	else {
		$data["error"] = "Unable to access this page, please try again.";
		return redirect()->view("login.php", $data);
	}
}
~~~

You can apply early exit on false positive like this:
~~~php
function isUserRole($id) {
	$utilModel = new utilFunction();
	$valid = $utilModel->checkUserExist($id);
	if(!$valid) {
		$data["error"] = "Unable to access this page, please try again.";
		return redirect()->view("login.php", $data);
	}
	$userModel = new userModel();
	$user_role = $userModel->userRole($id);
	if($user_role !== "admin") {
		$data["error"] = "Unable to access this page, please try again.";
		return redirect()->view("login.php", $data);
	}
	return true;
}
~~~

4) Do not comment your code to explain what is the purpose unless there is special cases that requires it. Because comment can be outdated due to requirement changes which means programmers have to remember to update comment. Your code should be the context needed to understand what is going on. Therefore be more clear or expressive on your naming, structure etc. There are exceptions to everything, you can comment on something if its unusual solution.

5) Avoid long functions, unless it helps with readability. Extracting part of your function generally can help with readability. Ideally your functions shouldn't be longer than a page worth.

6) Avoid inline styling like below, styling should be done in css folder of CodeIgniter4. If your styling only applies to your module, you should create a custom css like "/public/css/{your_module_name}/{page}.css". Your class name "should-be-style-with-dash"
~~~html
<span style="font-size:12px;color:pink;">Hello World</span>
~~~

7) Failed actions should have error return or log to indicate to users or programmers. Silent errors are hard to for end user, therefore you should always have something like try, catch. 