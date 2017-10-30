//
//  RadialGradientLabel.swift
//
//  Created by Rajat Hooja on 10/30/17.
//  Copyright © 2017 Rajat Hooja. All rights reserved.
//
//
// combination of the following two gradient techniques:
// https://stackoverflow.com/questions/33754294/swift-how-to-create-a-non-pixelated-radial-gradients
// https://github.com/chroman/CRGradientLabel

import UIKit

class CRGradientLabel: UILabel {
    
    var gradientColors: NSArray = NSArray()
    
    override init(frame: CGRect) {
        super.init(frame: frame)
    }
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
    }
    
    override func draw(_ rect: CGRect)
    {
        let context: CGContext = UIGraphicsGetCurrentContext()!
        
        let colors: NSMutableArray = NSMutableArray()
        
        self.gradientColors.enumerateObjects({ object, index, stop in
            if (object as AnyObject).isKind(of: UIColor.self) {
                colors.add((object as AnyObject).cgColor)
            } else if CFGetTypeID(object as CFTypeRef) == CGColor.typeID {
                colors.add(object)
            } else {
                NSException(name: NSExceptionName(rawValue: "CRGradientLabelError"), reason: "Object in gradientColors array is not a UIColor or CGColorRef", userInfo: nil).raise()
            }
        })
        
        context.saveGState()
        context.scaleBy(x: 1.0, y: -1.0)
        context.translateBy(x: 0, y: -rect.size.height)
        
        let gradient: CGGradient = CGGradient(colorsSpace: CGColorSpaceCreateDeviceRGB(), colors: colors, locations: nil)!
        
        let center = CGPoint(x: self.bounds.width / 2.0, y: self.bounds.height / 2.0)
        
        // we want the gradient to fill the entire label, so make the radius twice the width
        let radius = self.bounds.width * 2
        
        context.drawRadialGradient(gradient, startCenter: center, startRadius: 0.0, endCenter: center, endRadius: radius, options: CGGradientDrawingOptions())
                
        context.restoreGState()
        
        super.draw(rect)
        
    }
    
}
