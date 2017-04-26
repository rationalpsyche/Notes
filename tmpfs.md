## mount

`mkdir -p tmp`
`mount|grep -q $(pwd)/tmp || sudo mount -t tmpfs -o mode=01777,size=20m tmpfs tmp`

## unmount

`mount|grep -q $(pwd)/tmp || exit 0`
`sudo umount tmp`
`rm -f tmp`