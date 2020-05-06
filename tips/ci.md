# CI tips

### CircleCI :: generate list failed tests
```JavaScript
let failed_tests = document.querySelectorAll('ul li')
let failed_tests_text = '';
failed_tests.forEach((item, index) => {
  let fail_el = item.querySelector('header > div');
  if (fail_el !== null) {
    let test_name = fail_el.textContent.split(' - ');
    failed_tests_text += test_name[1] + '.' + test_name[0] + "\n";
  }
})
console.log(failed_tests_text);
```
