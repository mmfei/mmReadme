cd $GOPATH/src;
mkdir -p github.com/golang;
cd github.com/golang;
git clone https://github.com/golang/net;
ln -s $GOPATH/src/github.com/golang/net/ $GOPATH/src/golang.org/x/;
go install golang.org/x/net/html;
