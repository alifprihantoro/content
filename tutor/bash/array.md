## Array in Bash
### define var
```bash
FOO=(
  'array1'
  'array2'
)
FOO+=('array3')
```
### split with `\n\r`
input :
```bash
local LIST_FOO=$(printf '%s\n' "${FOO[@]}")
echo $LIST_FOO
```
output :
```txt
array1
array2
array3
```
### loop
```bash
for element in "${FOO[@]}"
do
  echo "Current element: $element"
done

# Print the final array (optional)
echo "Final array content:"
echo "${FOO[@]}"

```
output :
```txt
Current element: array1
Current element: array2
Current element: array3
Final array content:
array1 array2 array3
```
### contains VAR
input :
```bash
BAR='array1'
if [[ "${FOO[@]}" =~ "$bar" ]]; then
  echo "Found '$bar' in the FOO array"
else
  echo " '$bar' not found in the FOO array."
fi
```
output :
```txt
Found 'array1' in the FOO array
```