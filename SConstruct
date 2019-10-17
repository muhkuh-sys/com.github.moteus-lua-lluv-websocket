# -*- coding: utf-8 -*-
#-------------------------------------------------------------------------#
#   Copyright (C) 2019 by Christoph Thelen                                #
#   doc_bacardi@users.sourceforge.net                                     #
#                                                                         #
#   This program is free software; you can redistribute it and/or modify  #
#   it under the terms of the GNU General Public License as published by  #
#   the Free Software Foundation; either version 2 of the License, or     #
#   (at your option) any later version.                                   #
#                                                                         #
#   This program is distributed in the hope that it will be useful,       #
#   but WITHOUT ANY WARRANTY; without even the implied warranty of        #
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         #
#   GNU General Public License for more details.                          #
#                                                                         #
#   You should have received a copy of the GNU General Public License     #
#   along with this program; if not, write to the                         #
#   Free Software Foundation, Inc.,                                       #
#   59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.             #
#-------------------------------------------------------------------------#


#----------------------------------------------------------------------------
#
# Set up the Muhkuh Build System.
#

SConscript('mbs/SConscript')
Import('atEnv')

import os.path
import zipfile


#----------------------------------------------------------------------------
#
# Depack the source archive.
#
tSrcArchive = zipfile.ZipFile('lua-lluv-websocket-master.zip', 'r')
tSrcArchive.extractall('targets/depack')
tSrcArchive.close()
strDepackPath = 'targets/depack/lua-lluv-websocket-master/'

#----------------------------------------------------------------------------
#
# Build the artifacts.
#

strGroup = 'com.github.moteus'
strModule = 'lua-lluv-websocket'

# Split the group by dots.
aGroup = strGroup.split('.')
# Build the path for all artifacts.
strModulePath = 'targets/repository/%s/%s/%s' % ('/'.join(aGroup), strModule, PROJECT_VERSION)

# Set the name of the artifact.
strArtifact = 'lua-lluv-websocket'

tArcList = atEnv.DEFAULT.ArchiveList('zip')

tArcList.AddFiles('',
                    'installer/install.lua')

tArcList.AddFiles('lua/lluv',
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket.lua'))

tArcList.AddFiles('lua/lluv/websocket/',
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'utf8.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'bit.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'tools.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'frame.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'error.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'split.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'handshake.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'luasocket.lua'),
                  os.path.join(strDepackPath, 'src', 'lluv', 'websocket', 'utf8_validator.lua'))


tArtifact = atEnv.DEFAULT.Archive(os.path.join(strModulePath, '%s-%s.zip' % (strArtifact, PROJECT_VERSION)), None, ARCHIVE_CONTENTS = tArcList)
tArtifactHash = atEnv.DEFAULT.Hash('%s.hash' % tArtifact[0].get_path(), tArtifact[0].get_path(), HASH_ALGORITHM='md5,sha1,sha224,sha256,sha384,sha512', HASH_TEMPLATE='${ID_UC}:${HASH}\n')
tConfiguration = atEnv.DEFAULT.Version(os.path.join(strModulePath, '%s-%s.xml' % (strArtifact, PROJECT_VERSION)), 'installer/%s.xml' % strModule)
tConfigurationHash = atEnv.DEFAULT.Hash('%s.hash' % tConfiguration[0].get_path(), tConfiguration[0].get_path(), HASH_ALGORITHM='md5,sha1,sha224,sha256,sha384,sha512', HASH_TEMPLATE='${ID_UC}:${HASH}\n')
tArtifactPom = atEnv.DEFAULT.ArtifactVersion(os.path.join(strModulePath, '%s-%s.pom' % (strArtifact, PROJECT_VERSION)), 'installer/pom.xml')
