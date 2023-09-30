function setName()
    return "Target ESP"
end

local rotationAngle = 0
local moveOffset = 0
local moveSpeed = 1

function onEvent(event)
    if event:getName() == "render_event" then
        if event:is2D() then


            if auraTarget.isActiveTarget() then
                pos = project.projection(auraTarget.getPosition()[1], auraTarget.getPosition()[2] + 1, auraTarget.getPosition()[3])
                gl11.pushMatrix()

                rotationAngle = (rotationAngle + 1) % 360
                moveOffset = moveOffset + moveSpeed
                if moveOffset > 50 or moveOffset < -50 then
                    moveSpeed = -moveSpeed
                end

                gl11.position(pos[1] + moveOffset, pos[2], 0)
                gl11.rotate(rotationAngle, 0, 0, 1)
                gl11.position(-(pos[1] + moveOffset), -(pos[2]), 0)

                gl11.color(color.get(0))
                display.drawImage("https://cdn.discordapp.com/attachments/1153013127215058994/1157029626342821948/target.png?ex=65171f4f&is=6515cdcf&hm=981f231275f5671894b716a9726d263b23267772a84d4a2e1640f51f33a236fe&", pos[1] - 50, pos[2] - 50, 100, 100)
                gl11.popMatrix()
            end
        end
    end
end- 
