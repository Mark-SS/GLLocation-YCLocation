GLLocation-YCLocation
=====================

地球坐标，火星坐标，百度坐标系之间的转化

从 CLLocationManager 取出来的经纬度放到 mapView 上显示，是错误的!
 从 CLLocationManager 取出来的经纬度去 Google Maps API 做逆地址解析，当然是错的！
 从 MKMapView 取出来的经纬度去 Google Maps API 做逆地址解析终于对了。去百度地图API做逆地址解析，依旧是错的！
 从上面两处取的经纬度放到百度地图上显示都是错的！错的！的！
 
 分为 地球坐标，火星坐标（iOS mapView 高德 ， 国内google ,搜搜、阿里云 都是火星坐标），百度坐标(百度地图数据主要都是四维图新提供的)
 
 火星坐标: MKMapView
 地球坐标: CLLocationManager
 
 当用到CLLocationManager 得到的数据转化为火星坐标, MKMapView不用处理
 
 
 API                坐标系
 百度地图API         百度坐标
 腾讯搜搜地图API      火星坐标
 搜狐搜狗地图API      搜狗坐标
 阿里云地图API       火星坐标
 图吧MapBar地图API   图吧坐标
 高德MapABC地图API   火星坐标
 灵图51ditu地图API   火星坐标
 
 ```swift
override init(frame: CGRect) {
    super.init(frame: frame)
 
    trackLayer.backgroundColor = UIColor.blueColor().CGColor
    layer.addSublayer(trackLayer)
 
    lowerThumbLayer.backgroundColor = UIColor.greenColor().CGColor
    layer.addSublayer(lowerThumbLayer)
 
    upperThumbLayer.backgroundColor = UIColor.greenColor().CGColor
    layer.addSublayer(upperThumbLayer)
 
    updateLayerFrames()
}
 
required init(coder: NSCoder) {
    super.init(coder: coder)
}
 
func updateLayerFrames() {
    trackLayer.frame = bounds.rectByInsetting(dx: 0.0, dy: bounds.height / 3)
    trackLayer.setNeedsDisplay()
 
    let lowerThumbCenter = CGFloat(positionForValue(lowerValue))
 
    lowerThumbLayer.frame = CGRect(x: lowerThumbCenter - thumbWidth / 2.0, y: 0.0,
      width: thumbWidth, height: thumbWidth)
    lowerThumbLayer.setNeedsDisplay()
 
    let upperThumbCenter = CGFloat(positionForValue(upperValue))
    upperThumbLayer.frame = CGRect(x: upperThumbCenter - thumbWidth / 2.0, y: 0.0,
        width: thumbWidth, height: thumbWidth)
    upperThumbLayer.setNeedsDisplay()
}
 
func positionForValue(value: Double) -> Double {
    let widthDouble = Double(thumbWidth)
    return Double(bounds.width - thumbWidth) * (value - minimumValue) /
        (maximumValue - minimumValue) + Double(thumbWidth / 2.0)
}
```
