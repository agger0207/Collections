## objc_getAssociatedObject

- (AFHTTPRequestOperation *)af_imageRequestOperation {
    return (AFHTTPRequestOperation *)objc_getAssociatedObject(self, @selector(af_imageRequestOperation));
}

可以参考，直接使用@selector, 因为这个肯定是唯一的; 这个很早之前Matt就在NSHispter上说过